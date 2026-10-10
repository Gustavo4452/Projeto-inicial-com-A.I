# Vendas em foco — dashboard de análise

Dashboard educacional para a disciplina de Fundamentos de IA e Análise de Dados. O projeto usa apenas HTML, CSS e JavaScript puro, com Chart.js e Papa Parse carregados por CDN.

## Como executar

1. Abra `public/index.html` no navegador. A base demonstrativa já está incorporada no `public/script.js`, portanto o painel funciona mesmo sem um servidor local.
2. Para usar outra base, clique em **Importar CSV** e selecione um arquivo no computador. A leitura acontece localmente no navegador; o arquivo não é enviado para um servidor.
3. Use os filtros, a pesquisa da tabela e os cabeçalhos para ordenar. **Exportar CSV** baixa apenas os registros filtrados.

As bibliotecas externas são carregadas pela internet: Chart.js `4.4.4` e Papa Parse `5.4.1`. Sem conexão, os gráficos e a importação CSV podem não carregar.

O título está configurado para usar a fonte `Garet` quando ela estiver instalada no computador, com fallback para `DM Sans` e `Space Grotesk`. O arquivo da fonte não foi incorporado ao projeto; sem a fonte instalada, o navegador usará automaticamente uma das alternativas.

## Base e adaptação

O projeto original possui `vendas_hamburgueria.csv`, que foi preservado na raiz. Ele tem 1.367 linhas válidas, entre 01/07/2026 e 30/09/2026, e as colunas `id_venda`, `data`, `dia_semana`, `periodo`, `produto`, `categoria`, `quantidade`, `preco_unitario`, `forma_pagamento`, `canal`, `tempo_espera_min` e `avaliacao`.

Como essa base não contém `regiao`, a análise foi adaptada para comparar o faturamento por semana, com semanas iniciando na segunda-feira. Nenhuma região foi criada artificialmente.

`public/dados-exemplo.csv` é uma cópia da base fornecida e a mesma base está embutida no JavaScript para permitir a abertura direta do HTML. A interface identifica os dados como demonstrativos.

## Indicadores e regras

- Faturamento da linha = `quantidade × preco_unitario`.
- Faturamento total = soma do faturamento das linhas filtradas.
- Quantidade de vendas = quantidade de `id_venda` únicos.
- Unidades vendidas = soma de `quantidade`.
- Ticket médio = faturamento total ÷ quantidade de vendas; quando não há vendas, o resultado é `R$ 0,00`.

Datas precisam estar no formato `AAAA-MM-DD`. Linhas com ID ausente, data inválida, quantidade/preço ausente ou inválido, ou valores negativos são descartadas e a quantidade aparece no rodapé. Valores zero são aceitos e não são tratados como ausentes. Duplicatas não são removidas, pois cada linha representa uma venda e o significado de eventuais repetições deve ser confirmado pelo responsável pela base.

## Publicar no Render pelo GitHub

1. Envie o projeto para um repositório no GitHub, mantendo a pasta `public` e os arquivos da raiz.
2. No Render, crie um novo serviço **Static Site** e selecione o repositório.
3. Configure:
   - **Branch:** a branch que contém o projeto.
   - **Root Directory:** deixe vazio.
   - **Build Command:** `echo "Site pronto"`
   - **Publish Directory:** `public`
4. Clique em **Create Static Site**. O Render publicará o `public/index.html` e os arquivos relativos.

## Estrutura

```text
AGENTS.MD
README.md
vendas_hamburgueria.csv       # arquivo original preservado
public/
  index.html
  styles.css
  script.js
  dados-exemplo.csv
```

## Verificação

O código foi revisado para conferir o cálculo conhecido de cada linha (`quantidade × preco_unitario`), filtros combinados, limpeza dos filtros, ausência de resultados, pesquisa, ordenação, importação local e exportação CSV. Também foram conferidos os breakpoints de layout para telas grandes e pequenas por inspeção do CSS. Não foi possível executar um navegador gráfico nesta sessão; por isso, a inspeção visual e o console do navegador devem ser confirmados ao abrir a página localmente.
