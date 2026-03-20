# Ficha de Cadastro — modelo em Markdown para verificação de consistência de preenchimento

## Finalidade
Este arquivo converte a ficha de cadastro em um **modelo textual neutro**, sem reprodução dos dados do requerente, para permitir a verificação de:
- preenchimento de campos obrigatórios;
- coerência interna entre campos correlatos;
- padronização de nomes, endereços, contatos e documentos;
- consistência de coordenadas, áreas e unidades de medida.

---

## 1. DADOS DA EMPRESA

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 01. Empresa | `[preencher]` | Verificar se o nome está completo e sem abreviações, se essa for a exigência do formulário. |
| 02. Endereço da sede | `[preencher]` | Verificar se o logradouro foi informado de forma completa. |
| 03. Número | `[preencher]` | Verificar se há número ou, quando cabível, indicação expressa de “s/n”. |
| 04. Complemento | `[preencher]` | Verificar se o campo foi preenchido quando necessário. |
| 05. Bairro | `[preencher]` | Verificar uniformidade de grafia com os demais documentos do processo. |
| 06. Município | `[preencher]` | Verificar compatibilidade com o endereço informado. |
| 07. UF | `[preencher]` | Verificar se a sigla está correta. |
| 08. CEP | `[preencher]` | Verificar formato e compatibilidade com o endereço. |
| 09. DDD + Telefone | `[preencher]` | Verificar padronização e completude. |
| 10. CNPJ/MF (Sede) | `[preencher]` | Verificar formato, validade e correspondência com a pessoa jurídica indicada. |
| 11. Correio eletrônico | `[preencher]` | Verificar formato do e-mail e coerência institucional. |

---

## 2. RESPONSÁVEL PELA EMPRESA

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 12. Nome do responsável pela empresa | `[preencher]` | Verificar grafia uniforme em todos os documentos e campos correlatos. |
| 13. Cargo | `[preencher]` | Verificar se o cargo é compatível com a representação exercida. |
| 14. Telefone fixo e celular | `[preencher]` | Verificar padronização e completude. |
| 15. Correio eletrônico | `[preencher]` | Verificar formato e pertinência. |

---

## 3. DADOS DO TERMINAL

### 3.1. Coordenadas

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 16. Ponto central do terminal — latitude em graus decimais | `[preencher]` | Verificar se foi informado **ponto central**, e não vértices; verificar se a unidade está em **graus decimais**; verificar se o campo contém apenas latitude. |
| 17. Ponto central do terminal — longitude em graus decimais | `[preencher]` | Verificar se foi informado **ponto central**, e não vértices; verificar se a unidade está em **graus decimais**; verificar se o campo contém apenas longitude. |

### 3.2. Identificação e endereço do terminal

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 18. Nome do terminal | `[preencher]` | Verificar correspondência com nome fantasia ou denominação adotada no processo. |
| 19. Endereço do terminal | `[preencher]` | Verificar completude do logradouro. |
| 20. Número | `[preencher]` | Verificar se há número ou, quando cabível, indicação expressa de “s/n”. |
| 21. Complemento | `[preencher]` | Verificar necessidade do preenchimento. |
| 22. Bairro | `[preencher]` | Verificar uniformidade de grafia com os demais documentos. |
| 23. Município | `[preencher]` | Verificar compatibilidade com o endereço do terminal. |
| 24. UF | `[preencher]` | Verificar se a sigla está correta. |
| 25. CEP | `[preencher]` | Verificar formato e compatibilidade com o endereço. |
| 26. DDD + Telefone | `[preencher]` | Verificar padronização e completude. |
| 27. CNPJ/MF (Terminal) | `[preencher]` | Verificar se corresponde ao CNPJ exigido pelo formulário, inclusive quanto à matriz ou filial, quando aplicável. |
| 28. Correio eletrônico (terminal) | `[preencher]` | Verificar formato e coerência institucional. |

### 3.3. Responsável pelo terminal

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 29. Nome do responsável pelo terminal | `[preencher]` | Verificar uniformidade com procurações, atos societários e demais campos da ficha. |
| 30. Cargo | `[preencher]` | Verificar compatibilidade com a representação informada. |
| 31. Telefone fixo e celular | `[preencher]` | Verificar padronização e completude. |
| 32. Correio eletrônico (responsável) | `[preencher]` | Verificar formato e pertinência. |

---

## 4. DADOS FÍSICOS E OPERACIONAIS DO TERMINAL

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 33. Capacidade de armazenagem (estática) | `[preencher]` | Verificar se a unidade de medida é compatível com o conceito de capacidade estática. |
| 34. Área do terreno (m²) — alodial | `[preencher]` | Verificar formato numérico e coerência documental. |
| 35. Área em terra aforada (m²) | `[preencher]` | Verificar formato numérico e coerência documental. |
| 36. Área em terra do terminal (m²) (34 + 35) | `[preencher]` | Verificar se corresponde exatamente ao somatório dos itens 34 e 35. |
| 37. Área de acostagem (m²) | `[preencher]` | Verificar formato numérico e coerência documental. |
| 38. Área total (m²) (36 + 37) | `[preencher]` | Verificar se corresponde exatamente ao somatório dos itens 36 e 37. |

---

## 5. INVESTIMENTOS E MOVIMENTAÇÃO

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 39. Prazo de execução dos investimentos indicados | `[preencher]` | Verificar clareza da unidade temporal, como meses ou anos. |
| 40. Valor global do investimento | `[preencher]` | Verificar formato monetário e compatibilidade com os demais documentos do processo. |
| 41. Modalidade da instalação portuária | `[preencher]` | Verificar compatibilidade com o enquadramento jurídico do pedido. |
| 42. Estimativa de movimentação de carga geral (ton/ano) | `[preencher]` | Verificar unidade e coerência técnica. |
| 43. Estimativa de movimentação de granel sólido (ton/ano) | `[preencher]` | Verificar se o campo foi efetivamente preenchido ou se houve indicação expressa de não aplicação. |
| 44. Estimativa de movimentação de granel líquido (m³/ano) | `[preencher]` | Verificar se o campo foi efetivamente preenchido ou se houve indicação expressa de não aplicação. |
| 45. Estimativa de movimentação de contêiner (TEU/ano) | `[preencher]` | Verificar unidade e coerência técnica. |
| 46. Estimativa de movimentação de passageiros (passageiros/ano) | `[preencher]` | Verificar se o campo foi efetivamente preenchido ou se houve indicação expressa de não aplicação. |

---

## 6. OUTRAS INFORMAÇÕES

| Campo | Preenchimento | Critério de verificação |
|---|---|---|
| 47. Local, data | `[preencher]` | Verificar se a data é compatível com a assinatura e com os demais documentos do processo. |
| Assinatura | `[preencher]` | Verificar se a assinatura corresponde ao responsável indicado. |

---

## 7. INSTRUÇÕES DE PREENCHIMENTO TRANSCRITAS DA FICHA

1. Nome completo da empresa interessada, sem abreviações.  
2 a 8. Endereço completo da sede da empresa.  
9. Telefone da empresa.  
10. Número de inscrição da empresa (sede) no Ministério da Fazenda.  
11. Endereço eletrônico da sede da empresa.  
12 a 15. Dados do responsável pela empresa (sede).  
18. Nome pelo qual o terminal é conhecido (nome fantasia).  
19 a 25. Endereço completo do terminal.  
26. Telefone do terminal.  
27. Número de inscrição do terminal no Ministério da Fazenda (nº da filial).  
28. Endereço eletrônico do terminal.  
29 a 32. Dados do responsável pelo terminal (filial).  
33. Capacidade de armazenagem do terminal.  
34. Área do terreno “livre de foros, vínculos, pensões e ônus” (alodial).  
35. Área de terra cujo uso é permitido mediante pagamento de um foro anual.  
36. Somatório dos itens 34 e 35.  
37. Área de acostagem do terminal.  
38. Somatório dos itens 36 e 37.  
39. Prazo de execução dos investimentos para construção do Terminal.  
40. Valor global do investimento (valor venal) – terminais construídos.  

---

## 8. REGRAS OBJETIVAS DE VALIDAÇÃO

### 8.1. Identificação
- [ ] O nome da empresa está completo e sem abreviações, quando essa exigência constar da ficha.
- [ ] O CNPJ da sede está formalmente correto.
- [ ] O CNPJ do terminal está compatível com a instrução do campo.
- [ ] O nome do responsável está uniforme em todos os pontos da ficha.

### 8.2. Endereço e contato
- [ ] O endereço da sede está completo.
- [ ] O endereço do terminal está completo.
- [ ] O bairro está grafado de forma uniforme em todos os campos.
- [ ] O CEP está em formato correto.
- [ ] Os telefones estão padronizados.
- [ ] Os e-mails estão corretos.

### 8.3. Coordenadas
- [ ] Foi informado efetivamente o ponto central do terminal.
- [ ] As coordenadas estão em graus decimais.
- [ ] Não houve mistura entre latitude e longitude no mesmo campo.
- [ ] Não foram lançados vértices quando o formulário exige ponto central.

### 8.4. Áreas
- [ ] O item 36 corresponde ao somatório dos itens 34 e 35.
- [ ] O item 38 corresponde ao somatório dos itens 36 e 37.
- [ ] As unidades de área estão uniformes.

### 8.5. Capacidade e movimentação
- [ ] A unidade da capacidade de armazenagem é tecnicamente compatível com o campo.
- [ ] As estimativas de movimentação utilizam as unidades corretas.
- [ ] Campos não aplicáveis estão identificados de maneira padronizada.

---

## 9. CAMPO PARA REGISTRO DE INCONSISTÊNCIAS ENCONTRADAS

### Inconsistência 1
- Campo:
- Descrição:
- Tipo de problema:
- Providência sugerida:

### Inconsistência 2
- Campo:
- Descrição:
- Tipo de problema:
- Providência sugerida:

### Inconsistência 3
- Campo:
- Descrição:
- Tipo de problema:
- Providência sugerida:

### Inconsistência 4
- Campo:
- Descrição:
- Tipo de problema:
- Providência sugerida:
