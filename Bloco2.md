# Bloco2 - FLEXBILL / Requisitos funcionais e contábeis

> Versão revisada e reorganizada do conteúdo extraído do PDF em Markdown.

## 1. Visão geral

Este documento reúne requisitos funcionais e operacionais relacionados ao cenário Flexbill para dois artefatos principais:

- Relatórios contábeis BRM - FLX
- Interface contábil de faturado Flexbill pós-pago TBRA

O objetivo comum é garantir que os registros classificados como Flexbill sejam tratados de forma segregada, mantendo compatibilidade com os processos já existentes.

## 2. Contexto e objetivo

### 2.1 Relatórios contábeis BRM - FLX

Foram previstos dois novos relatórios mensais:

- Relatório Faturado BRM - FLX
- Relatório Faturamento por Cliente (Analítico) BRM - FLX

Esses relatórios devem ser gerados a partir de views BRM específicas, com layout aderente a modelos aprovados e disponibilidade no diretório padrão da contabilidade para consumo via Control-M e BI Publisher.

### 2.2 Interface contábil Flexbill pós-pago TBRA

Foi definida uma nova interface contábil mensal para processamento no SAP, baseada no layout da família BFAT, com segregação do faturamento Flexbill em relação ao cenário AS IS.

## 3. Escopo

### 3.1 Incluído

- Criação/adequação dos relatórios BRM - FLX
- Adequação dos processos de seleção e extração contábil
- Geração mensal de arquivos com regras de filtro Flexbill
- Disponibilização operacional em diretórios e mecanismos já existentes

### 3.2 Fora do escopo

- Faturamento para cliente estrangeiro, tratado em US apartada
- Alteração do layout de interfaces já existentes, além do suporte ao novo cenário Flexbill
- Alteração da periodicidade, da janela operacional e da consolidação de interfaces não contempladas na US

## 4. Premissas, pré-condições e restrições

### Pré-condições

- As views de origem devem estar disponíveis no ambiente.
- A janela operacional mensal deve estar definida.
- A estrutura operacional de publicação deve existir (diretório padrão da contabilidade, Control-M, BI Publisher).
- Os processos `pin_mta_selecao_contabil`, `c_extracao_contabil` e seus scripts/jobs devem estar disponíveis para adequação.

### Premissas

- Um registro é considerado Flexbill quando possui `billing_segment = 105` e/ou marcação Flexbill em `account` ou `billinfo`.
- Os novos artefatos devem utilizar apenas registros classificados como Flexbill.
- Os relatórios e interfaces devem preservar compatibilidade operacional com os processos atuais.

### Restrições

- Não deve haver dependência de tabelas customizadas das interfaces para a geração dos novos artefatos.
- O comportamento atual das interfaces e relatórios já existentes deve ser preservado.
- A janela operacional mensal deve ser respeitada.

## 5. Regras de negócio

- Apenas registros classificados como Flexbill devem aparecer nos novos relatórios/interfaces.
- A janela operacional considerada deve ser de 26 do mês anterior até 25 do mês vigente.
- A geração deve ocorrer no dia 26 do mês corrente, a partir das 00h.
- A disponibilização dos artefatos deve ocorrer no mesmo dia, em formato compatível com os processos operacionais.

## 6. Requisitos funcionais

### 6.1 Relatórios BRM - FLX

- Utilizar as views específicas definidas como fonte oficial para cada relatório.
- Preservar fidelidade dos dados retornados pelas views.
- Aplicar a regra de exclusão/seleção dos registros Flexbill.
- Gerar arquivos com nomenclatura padronizada e layout previsto.
- Disponibilizar os arquivos via Control-M e BI Publisher.

### 6.2 Interface contábil Flexbill TBRA

- Adequar os processos de seleção e extração contábil para o novo cenário.
- Suportar a interface `TBRAYYYYBFATFLX999` no contexto Flexbill pós-pago TBRA.
- Reutilizar o layout da família BFAT, com referência em arquivos como `TBRA2026BFAT178.txt` e `TBRA2026BFAT181.txt`.
- Gerar uma interface mensal segregada do faturamento AS IS para processamento contábil no SAP.

## 7. Requisitos não funcionais

- Preservar estrutura tabular e layout dos modelos aprovados.
- Manter rastreabilidade entre os dados exibidos e as views de origem.
- Garantir compatibilidade com os processos operacionais e de integração.
- Evitar regressão funcional nas interfaces e relatórios já existentes.

## 8. Sistemas impactados

- Views BRM específicas
- Processos de seleção e extração contábil
- Scripts associados
- Jobs no Control-M
- BI Publisher
- SAP

## 9. Critérios de aceite

- As views e a janela operacional devem estar disponíveis.
- Os processos e jobs devem executar corretamente para a referência mensal definida.
- Somente registros classificados como Flexbill devem ser selecionados.
- Os arquivos gerados devem seguir layout, nomeação e estrutura definidos.
- A implementação não deve causar regressão nas interfaces e relatórios já existentes.
