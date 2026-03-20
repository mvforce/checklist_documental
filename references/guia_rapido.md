# Guia Rápido — Manutenção e Expansão da Skill checklist-resolucao-71

## Estrutura de arquivos

```
checklist-resolucao-71/
├── SKILL.md                                    ← Motor universal (não alterar sem revisão cuidadosa)
├── checklists/
│   └── resolucao71/                            ← Módulo: TUP/ETC/IPTUR Construção/Exploração
│       ├── lista_itens.md                      ← Lista fixa de itens (fonte normativa operacional)
│       └── ficha_cadastro_template.md          ← Template de referência para o item A.1
└── references/
    └── guia_rapido.md                          ← Este arquivo
```

---

## O que é o motor e o que são os módulos

**Motor (SKILL.md):** contém as regras de classificação, validade, determinismo, formato de saída e restrições. É universal. Não deve ser alterado para acomodar peculiaridades de um tipo específico de processo. Alterações no motor afetam todos os tipos de processo.

**Módulos (subdiretórios em `checklists/`):** contêm os itens específicos de cada tipo de processo. São intercambiáveis. Cada módulo contém ao menos um arquivo `lista_itens.md`.

---

## Como adicionar um novo tipo de processo

### Passo a passo

1. Criar subdiretório: `checklists/[nome_do_novo_modulo]/`
2. Criar `lista_itens.md` nesse subdiretório, seguindo o mesmo padrão de formatação do módulo `resolucao71`.
3. Se o novo processo tiver formulário-padrão com template de verificação: criar o arquivo correspondente (ex.: `ficha_cadastro_template.md`) no mesmo subdiretório.
4. Atualizar a tabela de tipos de processo no PASSO 1 do `SKILL.md`, adicionando uma linha para o novo módulo.

### Convenções de nomenclatura

| Elemento | Convenção |
|---|---|
| Nome do subdiretório | snake_case, descritivo (ex.: `renovacao_autorizacao`, `transferencia_titularidade`) |
| Arquivo de lista de itens | sempre `lista_itens.md` |
| Arquivo de template de formulário | sempre `ficha_cadastro_template.md` ou nome descritivo |

---

## O que NÃO alterar no motor

As seguintes seções do `SKILL.md` são críticas para o determinismo e não devem ser alteradas sem revisão formal:

- Regras de determinação da `{{data_referencia}}`
- As quatro classificações (Sim / Não / Possivelmente incorreto / N/A) e seus critérios
- O escopo de verificação (presença, identificabilidade, validade temporal)
- O formato obrigatório de saída (seções 5.1 a 5.5)
- As restrições globais

---

## O que PODE ser alterado no motor com cautela

- Tabela de tipos de processo no PASSO 1 (expansão de módulos).
- Dicionário de certidões (seção 2.6) — apenas para adição de novas palavras-chave literais comprovadas.
- Prazos de validade presumida (seção 2.7) — apenas se houver alteração normativa expressa.

---

## Módulos existentes

| Módulo | Tipo de processo | Base normativa | Arquivo principal |
|---|---|---|---|
| `resolucao71` | TUP / ETC / IPTUR — Construção/Exploração | Resolução ANTAQ nº 71/2022, art. 4º | `lista_itens.md` |

---

## Observações sobre o item A.1 (Ficha de Cadastro)

O item A.1 do módulo `resolucao71` exige verificação de conformidade da ficha de cadastro com o template de referência. Essa verificação utiliza o arquivo `ficha_cadastro_template.md`, que contém:

- modelo dos campos obrigatórios
- critérios de verificação por campo
- regras de validação de áreas (somatórios)
- regras de validação de coordenadas

A verificação da ficha de cadastro é limitada pelo escopo do motor: presença dos campos, identificabilidade e consistência formal dos dados (ex.: somatório de áreas). O motor **não verifica** a veracidade das informações declaradas.

---

## Sinalizações especiais herdadas do módulo resolucao71

O módulo `resolucao71` contém dois itens com tratamento especial, definidos na lista de itens:

- **D.9 (Item IX)** e **D.19 (Item XVIII)**: marcados como "não se aplica — não verificar". O motor os registra automaticamente como N/A sem necessidade de comprovação documental, pois a inaplicabilidade está expressa na própria lista normativa.

- **D.7 (Item VII)** — contrato de locação: quando localizado, o motor deve sinalizar que **o analista humano deve realizar análise detalhada do instrumento**, conforme regra de evidência específica do módulo.
