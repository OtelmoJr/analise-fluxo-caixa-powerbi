# Analise de Fluxo de Caixa no Power BI

Projeto de portifolio voltado a analise financeira, modelagem dimensional e construcao de dashboards executivos no Power BI.

O trabalho simula o fluxo de caixa de uma empresa de medio porte industrial e transforma dados operacionais brutos em uma camada analitica capaz de responder perguntas criticas de negocio, como:

- O caixa da empresa esta crescendo ou encolhendo ao longo do tempo?
- Quais grupos de contas pressionam mais as saidas?
- Como o saldo se distribui entre os bancos?
- Em quais meses a operacao perde folga financeira?

## Visao do dashboard

![Dashboard executivo DFC](assets/img/image2.jpg)

## Objetivo do projeto

Este projeto foi desenvolvido para demonstrar capacidade de:

- Estruturar um caso de negocio financeiro de ponta a ponta
- Modelar dados em estrela para analise no Power BI
- Criar medidas DAX orientadas a tomada de decisao
- Traduzir indicadores financeiros em visuais executivos e analiticos
- Documentar um projeto de BI com clareza para portfolio tecnico

## Problema de negocio

Muitas empresas ainda controlam fluxo de caixa em planilhas dispersas, com alto risco de erro manual, baixa rastreabilidade e dificuldade para consolidar dados por banco, conta e periodo.

Neste contexto, a proposta da solucao foi centralizar os dados financeiros em um unico modelo analitico e entregar uma leitura gerencial sobre entradas, saidas, saldo operacional, saldo inicial e saldo final.

## Solucao entregue

O repositorio contem uma solucao de BI com:

- Base de dados bruta em CSV
- Modelo Power BI em [analise-fluxo-caixa-powerbi/fluxo-caixa.pbix](analise-fluxo-caixa-powerbi/fluxo-caixa.pbix)
- Estrutura dimensional com tabelas fato e dimensao
- Medidas DAX para os principais indicadores de caixa
- Dashboards com visao executiva e visao analitica

## Principais resultados

- Consolidacao de informacoes de 3 bancos, 27 contas e 5 grupos de fluxo em um unico modelo
- Automatizacao do calculo de saldo inicial, saldo operacional e saldo final
- Reducao do trabalho manual de consolidacao financeira
- Capacidade de analise por ano, mes, banco, grupo, subgrupo e conta
- Geracao de insights acionaveis a partir dos visuais

## Stack utilizada

| Tecnologia | Papel no projeto |
| --- | --- |
| Power BI Desktop | Modelagem, medidas e dashboards |
| Power Query | Ingestao, limpeza e transformacao dos dados |
| DAX | Calculos analiticos e indicadores |
| Git / GitHub | Versionamento e publicacao do portfolio |
| VS Code | Documentacao tecnica em Markdown |

## Arquitetura da solucao

| Camada | Componente | Descricao |
| --- | --- | --- |
| Dados brutos | CSVs | Bancos, PlanoContas, Movimentos, SaldoAnterior e Modelo |
| Transformacao | Power Query | Tipagem, limpeza e chaves de relacionamento |
| Modelo | Star Schema | `dim_bancos`, `dim_contas`, `dim_grupos`, `dim_calendario`, `f_movimentos`, `f_saldo_anterior` |
| Analise | DAX | Indicadores financeiros e logica de saldo |
| Visualizacao | Dashboards Power BI | Pagina executiva DFC e pagina analitica Matriz |

## Base de dados

Os arquivos de entrada estao em [analise-fluxo-caixa-powerbi/dados_brutos](analise-fluxo-caixa-powerbi/dados_brutos):

| Arquivo | Papel |
| --- | --- |
| [analise-fluxo-caixa-powerbi/dados_brutos/Bancos.csv](analise-fluxo-caixa-powerbi/dados_brutos/Bancos.csv) | Cadastro dos bancos |
| [analise-fluxo-caixa-powerbi/dados_brutos/PlanoContas.csv](analise-fluxo-caixa-powerbi/dados_brutos/PlanoContas.csv) | Hierarquia contabil |
| [analise-fluxo-caixa-powerbi/dados_brutos/Movimentos.csv](analise-fluxo-caixa-powerbi/dados_brutos/Movimentos.csv) | Transacoes financeiras |
| [analise-fluxo-caixa-powerbi/dados_brutos/SaldoAnterior.csv](analise-fluxo-caixa-powerbi/dados_brutos/SaldoAnterior.csv) | Saldo de abertura por banco |
| [analise-fluxo-caixa-powerbi/dados_brutos/Modelo.csv](analise-fluxo-caixa-powerbi/dados_brutos/Modelo.csv) | Estrutura do fluxo de caixa |

## Modelagem dimensional

O modelo foi estruturado em estrela para garantir simplicidade de navegacao, performance e manutencao analitica.

Relacionamentos principais:

- `dim_bancos` 1:N `f_movimentos`
- `dim_contas` 1:N `f_movimentos`
- `dim_calendario` 1:N `f_movimentos`
- `dim_bancos` 1:N `f_saldo_anterior`

Essa abordagem permite filtrar o fluxo de caixa por periodo, banco e classificacao contabil sem duplicidade de regra no dashboard.

## Indicadores construidos em DAX

As medidas centrais do projeto foram:

- `Entradas`
- `Saidas`
- `Saidas ABS`
- `Saldo Operacional`
- `Saldo Inicial`
- `Saldo Final`
- `Fluxo`

Exemplo de logica principal:

```text
Saldo Final = Saldo Inicial + Saldo Operacional
```

Essas medidas sustentam tanto os cards executivos quanto a matriz analitica detalhada.

## Galeria de telas

### Pagina executiva DFC

Visao consolidada com cards e graficos para leitura rapida do desempenho financeiro.

![Pagina executiva DFC](assets/img/image2.jpg)

### Pagina analitica Matriz

Visao detalhada com drill-down por grupo, subgrupo, conta, ano e mes.

![Pagina Matriz](assets/img/image3.jpg)

### Visuais de apoio

Entradas e saidas por periodo:

![Entradas e saidas por ano e mes](assets/img/image7.jpg)

Saldo acumulado por periodo:

![Saldo acumulado por ano e mes](assets/img/image6.jpg)

Saldo por banco:

![Saldo por banco](assets/img/image1.png)

Entradas por subgrupo:

![Entradas por subgrupo](assets/img/image5.png)

Saidas por subgrupo:

![Saidas por subgrupo](assets/img/image4.png)

## Insights de negocio destacados

- O saldo operacional consolidado do periodo analisado ficou negativo, indicando pressao recorrente das saidas sobre as entradas
- 2023 apresentou desempenho mais saudavel, enquanto 2024 mostrou deterioracao mais forte no caixa
- Pagamentos a fornecedores e despesas com pessoal aparecem como principais vetores de saida
- O Itau Unibanco concentrou o pior saldo entre os bancos analisados
- A maior parte das entradas veio de receitas com vendas, revelando baixa diversificacao de fontes de receita

## Estrutura do repositorio

```text
analise-fluxo-caixa-powerbi/
|-- assets/
|   `-- img/
|       |-- image1.png
|       |-- image2.jpg
|       |-- image3.jpg
|       |-- image4.png
|       |-- image5.png
|       |-- image6.jpg
|       `-- image7.jpg
|-- dados_brutos/
|   |-- Bancos.csv
|   |-- Modelo.csv
|   |-- Movimentos.csv
|   |-- PlanoContas.csv
|   `-- SaldoAnterior.csv
|-- documentacao-fluxo-caixa.docx
|-- fluxo-caixa.pbix
`-- README.md
```

## Como abrir o projeto

1. Abra [analise-fluxo-caixa-powerbi/fluxo-caixa.pbix](analise-fluxo-caixa-powerbi/fluxo-caixa.pbix) no Power BI Desktop.
2. Aponte as consultas para os arquivos em [analise-fluxo-caixa-powerbi/dados_brutos](analise-fluxo-caixa-powerbi/dados_brutos), se necessario.
3. Atualize o modelo.
4. Navegue entre a pagina executiva DFC e a pagina Matriz.

## Diferenciais para portfolio

Este projeto demonstra combinacao de repertorio tecnico e contexto de negocio:

- Pensamento analitico aplicado a financas
- Modelagem dimensional orientada a performance
- Traducao de regra de negocio em DAX
- Design de dashboard com foco executivo
- Documentacao pronta para recrutadores, clientes e avaliadores tecnicos
