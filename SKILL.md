---
name: checklist-resolucao-71
description: >
  Motor de verificação documental determinístico para processos administrativos da ANTAQ.
  Use esta skill sempre que o usuário enviar documentos de processo administrativo da ANTAQ
  para análise de regularidade documental, mencionar "checklist", "Resolução 71", "art. 4º",
  "habilitação", "documentação", "instrução processual", "TUP", "ETC", "IPTUR", "autorização
  portuária" ou pedir para "verificar documentos" em contexto aquaviário ou portuário.
  Também usar quando o usuário perguntar se um conjunto de arquivos está completo ou regular
  para fins de habilitação na ANTAQ, ou quando mencionar análise de processo com número no
  formato 50300.XXXXXX/AAAA-DD.
---

# Motor de Verificação Documental — ANTAQ

## Visão Geral

Esta skill implementa um motor de análise documental **determinístico e modular**.

O motor é fixo e está contido neste arquivo.  
Os **checklists** (listas de itens e templates) são módulos externos, trocáveis conforme o tipo de processo.

```
checklist-resolucao-71/
├── SKILL.md                         ← Motor (este arquivo)
├── checklists/
│   └── resolucao71/
│       ├── lista_itens.md           ← Lista fixa de itens do checklist
│       └── ficha_cadastro_template.md ← Template de referência da ficha cadastral
└── references/
    └── guia_rapido.md               ← Referência rápida para manutenção
```

---

## PASSO 1 — Identificar o tipo de processo e carregar o checklist correto

Antes de qualquer análise, identificar o tipo de processo a partir do contexto do usuário ou dos documentos recebidos.

| Tipo de processo | Checklist a carregar |
|---|---|
| TUP / ETC / IPTUR — Construção/Exploração (Resolução ANTAQ nº 71/2022) | `checklists/resolucao71/` |
| (outros tipos serão adicionados aqui conforme expansão da skill) | `checklists/[novo_modulo]/` |

**Ação obrigatória:** ler os dois arquivos do módulo correspondente antes de iniciar qualquer análise:
1. `lista_itens.md` — contém a lista fixa de itens e a ordem de verificação.
2. `ficha_cadastro_template.md` — contém o template de referência para o item A.1 (Ficha de Cadastro).

---

## PASSO 2 — Aplicar as regras do motor

As regras abaixo são **universais** e se aplicam a qualquer checklist carregado.

### 2.1 Premissas obrigatórias

1. Não usar inferência especulativa.
2. Não adivinhar.
3. Não utilizar conhecimento externo.
4. Não complementar lacunas documentais com probabilidade, costume administrativo ou suposição.
5. Basear-se apenas: (a) no conteúdo literal dos arquivos anexados; e (b) no checklist carregado.
6. Em caso de dúvida, insuficiência documental, ausência de data, ilegibilidade ou impossibilidade de confirmação segura: adotar classificação conservadora.

### 2.2 Escopo da verificação documental

O motor verifica **três dimensões e apenas três**:

| Dimensão | Descrição |
|---|---|
| **Presença** | O documento foi protocolado / está nos autos? |
| **Identificabilidade** | É identificável como o tipo exigido pelo item do checklist? |
| **Validade temporal** | Está dentro do prazo de validade, quando aplicável? |

**É expressamente vedado ao motor:**
- Examinar cláusulas contratuais.
- Verificar coerência técnica de plantas, memoriais descritivos ou orçamentos.
- Avaliar suficiência de conteúdo interno de documentos.
- Interpretar redação de atos societários ou procurações.

> Quando o item exigir análise de conteúdo que ultrapasse essas três dimensões, o motor deve registrar a limitação e sinalizar que **o analista humano deve realizar análise complementar**.

### 2.3 Determinação da data de referência ({{data_referencia}})

Extrair exclusivamente a partir do mais recente **Recibo Eletrônico de Protocolo** que contenha simultaneamente:
- Campo "Número do Processo:" no formato: `50300.\d{6}\/\d{4}-\d{2}`
- Campo "Data e Horário:"

**Regras:**
- Se houver mais de um recibo válido para o mesmo processo: usar o mais recente.
- Se não houver recibo válido com esses campos: `{{data_referencia}} = "NÃO ENCONTRADA"`.
- Nunca substituir o Recibo Eletrônico de Protocolo por outro documento para definir a data de referência.
- Se a data estiver truncada, ilegível ou incompleta: considerar "NÃO ENCONTRADA".

### 2.4 Leitura dos documentos

1. Ler **todos** os arquivos integralmente, página por página, em ordem linear.
2. Nunca pular páginas.
3. Aplicar OCR sempre que houver imagem, digitalização, baixa legibilidade ou trecho não textual.
4. Só iniciar o checklist após o encerramento da leitura completa de todos os arquivos.
5. Após a primeira leitura, executar **segunda varredura obrigatória** procurando explicitamente: CERTIDÃO, NEGATIVA, REGULARIDADE, FISCAL.
6. Se a segunda varredura encontrar evidências adicionais: atualizar os resultados antes da saída final.

**Índice documental interno** (criar durante a leitura):
- tipo_documento
- nome do arquivo
- página
- número SEI identificado
- palavras-chave relevantes
- datas relevantes encontradas
- indícios de validade
- item(s) potencialmente relacionado(s) do checklist

### 2.5 Extração de números SEI

Usar regex: `\b\d{7}\b`

- Registrar o SEI principal (preferencialmente o constante do nome do arquivo).
- Para cada item do checklist: informar o SEI do documento principal utilizado como evidência.
- Se nenhum SEI for localizado: informar "SEI não identificado".

### 2.6 Dicionário determinístico de certidões

Classificar certidões apenas com base em texto efetivamente presente no documento:

| Esfera | Palavras-chave literais |
|---|---|
| Fazenda Municipal | CERTIDÃO NEGATIVA / TRIBUTOS MUNICIPAIS / PREFEITURA |
| Fazenda Estadual | SEFAZ / CERTIDÃO ESTADUAL / REGULARIDADE ESTADUAL |
| Fazenda Federal | CERTIDÃO CONJUNTA / DÍVIDA ATIVA DA UNIÃO / REGULARIDADE FEDERAL |
| INSS | CERTIDÃO PREVIDENCIÁRIA |
| FGTS | CRF / CERTIFICADO DE REGULARIDADE |

Se o documento não contiver elementos literais suficientes para enquadramento seguro: tratar como evidência insuficiente. Não reclassificar por contexto.

### 2.7 Validade documental

**Quando houver validade expressa:** usar a primeira data após expressão de validade ("Válida até", "Validade", "Expira em", "Data limite").

**Quando não houver validade expressa, mas houver data de emissão:** aplicar validade presumida:
- Certidões fiscais (qualquer esfera): 180 dias
- FGTS (CRF): 30 dias
- Certidões falimentares: 90 dias

**Comparação com {{data_referencia}}:**
- `data_validade >= {{data_referencia}}` → válido
- `data_validade < {{data_referencia}}` → vencido
- `{{data_referencia}} = "NÃO ENCONTRADA"` → não classificar automaticamente como válido

**Situações de incerteza** (data ausente, ilegível, incompleta, desvinculada): classificar como "Possivelmente incorreto".

---

## PASSO 3 — Classificação dos itens

Aplicar **exclusivamente** as quatro classificações abaixo:

| Classificação | Condição |
|---|---|
| **Sim** | Documento localizado, legível, identificável como o tipo exigido, com conteúdo suficiente para comprovação das três dimensões verificáveis, e válido quando a validade for exigível. |
| **Não** | Documento exigido não localizado nos arquivos analisados, ou inexistência de evidência documental mínima. |
| **Possivelmente incorreto** | Documento existe, mas está vencido, ilegível, truncado, incompleto, sem datas essenciais, com contradição interna ou entre documentos, ou sem elementos bastantes para confirmação segura. |
| **N/A** | Inaplicabilidade comprovada de forma expressa e objetiva na norma ou em documento oficial dos autos. **Nunca usar por presunção. Em caso de dúvida entre N/A e outra classificação: não usar N/A.** |

**Regra central de segurança:** em qualquer dúvida, usar "Possivelmente incorreto", nunca "Sim" ou "N/A" por presunção.

---

## PASSO 4 — Ordem fixa de execução

1. Carregar os arquivos do módulo de checklist.
2. Identificar `{{data_referencia}}`.
3. Ler todos os arquivos integralmente.
4. Realizar a segunda varredura obrigatória.
5. Consolidar o índice documental.
6. Analisar os itens em ordem crescente, sem reordenação.
7. Produzir a tabela final.
8. Produzir o resultado geral.
9. Listar pendências.
10. Listar itens N/A.
11. Listar próximos passos recomendados.

**É vedado:** inverter a ordem, omitir item, agrupar itens, reordenar o relatório ou fundir classificações.

---

## PASSO 5 — Formato obrigatório de saída

### 5.1 Tabela Markdown

```
| Item | Descrição | Atendido? | SEI |
|------|-----------|-----------|-----|
| A.1  | [descrição literal do item] | Sim/Não/Possivelmente incorreto/N/A | [SEI ou "SEI não identificado"] |
```

- A ordem dos itens é fixa (conforme `lista_itens.md` do módulo carregado).
- A descrição deve ser retirada exclusivamente do checklist carregado.
- Não resumir nem reescrever livremente a descrição.
- O campo "Atendido?" deve conter exclusivamente uma das quatro classificações.

### 5.2 Resultado geral

```
TODOS OS ITENS DEVEM SER ATENDIDOS: SIM ou NÃO
```

Só é "SIM" se todos os itens, exceto os N/A, estiverem com "Sim". Qualquer outro cenário: "NÃO".

### 5.3 Pendências

Para cada item classificado como "Não" ou "Possivelmente incorreto":
- número do item
- descrição resumida
- motivo literal e objetivo da pendência

Não incluir comentários opinativos. Não sugerir regularização neste bloco.

### 5.4 Itens N/A

Para cada item N/A:
- número do item
- justificativa literal
- trecho da norma ou documento oficial que comprove a inaplicabilidade

Se não houver: escrever "Não há itens classificados como N/A."

### 5.5 Próximos passos recomendados

Indicar objetivamente o que falta apresentar, substituir ou regularizar. Os próximos passos devem derivar diretamente das pendências. Não incluir recomendações genéricas.

---

## Regras de evidência e contradição

1. Vincular cada item ao documento mais diretamente relacionado.
2. Se houver mais de um documento potencialmente aplicável:
   - Priorizar o mais específico.
   - Se houver documentos contraditórios: registrar a contradição.
   - Não escolher discricionariamente um como correto sem base textual objetiva.
3. Se a contradição impedir comprovação segura: "Possivelmente incorreto".
4. Ausência de comprovação documental não pode ser compensada por contexto.

---

## Restrições globais

É proibido:
1. Usar conhecimento externo.
2. Usar memória de conversas anteriores.
3. Alterar a estrutura do relatório.
4. Gerar conclusões sem texto literal de suporte.
5. Reordenar os itens do checklist.
6. Classificar como "Sim" sem confirmação documental suficiente.
7. Classificar como "N/A" por presunção.
8. Omitir limitações de leitura.
9. Suavizar inconsistências.
10. Variar o critério entre casos semelhantes.

---

## Como adicionar um novo tipo de processo

1. Criar subdiretório em `checklists/[nome_do_modulo]/`.
2. Criar `lista_itens.md` com a lista fixa de itens do novo processo.
3. Se houver formulário-padrão com template de verificação: criar `ficha_cadastro_template.md` (ou equivalente) no mesmo subdiretório.
4. Atualizar a tabela de tipos de processo no PASSO 1 deste arquivo.
5. O motor permanece inalterado.

> Para mais detalhes sobre manutenção e expansão, consultar `references/guia_rapido.md`.
