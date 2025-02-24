<h1>Vendas Gerais do Mercado de Jogos</h1>

<hr>

<h3><a href="https://app.powerbi.com/view?r=eyJrIjoiNjRiYzQ1MjMtZjQ3ZS00MzAzLWI1MjEtMmZhNDhkMjVjZmI2IiwidCI6IjBjM2IyYzljLWVlYTctNDJlZi04YTYzLTcwOWIyNjU5NzYxOCJ9"> Acesse o Dashboard aqui</a></h3>

<hr>

<h3>Objetivos</h3>

Analisar as vendas de videogames para identificar tendências, comparações e insights relevantes sobre o mercado de games.

A análise é voltada para identificar os seguintes aspectos:

- O panorama geral do mercado (vendas globais);

- Desempenho por plataforma, gênero, publicadora e regiões;

- Evolução das vendas ao longo dos anos;

<hr>

<h4>Essa análise abrange os seguintes aspectos:</h4>

- <b>Visão Geral:</b> Total de vendas e os principais jogos.

- <b>Análise por Plataforma:</b> Comparação de vendas entre as diversas plataformas de jogos.

- <b>Análise por Gênero:</b> Desempenho dos gêneros de jogos no mercado.

- <b>Análise por Desenvolvedora:</b> Identificação da publicadora desenvolvedora com maior volume de vendas.

- <b>Evolução Temporal:</b> Tendências de vendas ao longo do tempo.

- <b>Regiões de Venda:</b> Distribuição de vendas por regiões geográficas.

<hr>

<h4>Entendendo a base de dados</h4>

A fonte de dados que eu utilizei foi um arquivo simples separado por vírgulas (vgsales.csv) que contém informações sobre vendas de videogames. 

As principais colunas são:

- <b>Rank:</b> Posição do jogo no ranking de vendas.

- <b>Name:</b> Nome do jogo.

- <b>Platform:</b> Plataforma (por exemplo, Wii, NES, PS4, etc.).

- <b>Year:</b> Ano de lançamento do jogo.

- <b>Genre:</b> Gênero do jogo (por exemplo, Ação, Esportes, RPG).

- <b>Publisher:</b> Publicadora ou desenvolvedora responsável.

- <b>NA_Sales:</b> Vendas na América do Norte (em milhões).

- <b>EU_Sales:</b> Vendas na Europa (em milhões).

- <b>JP_Sales:</b> Vendas no Japão (em milhões).

- <b>Other_Sales:</b> Vendas em outras regiões (em milhões).

- <b>Global_Sales:</b> Soma de todas as regiões, representando as vendas globais.

<hr>

<h4>Estruturação do Relatório</h4>

O relatório é dividido em duas páginas contendo análises específicas.

<h2><b>Visão Geral</b></h2>

- Objetivo: Apresentar um panorama geral das vendas de videogames.

- Gráficos e Elementos contidos na página:

<b>Cartão</b>

Medida em DAX contida no gráfico:

```python
TotalVendasGlobais = SUM(vgsales[Global_Sales])
#Exibe a soma total de todas as vendas globais.
```

<hr>

<b>Cartão</b>

Exibe o Gênero de jogo mais vendido

Medida em DAX contida no Gráfico:

```python
Genero Mais Vendido = 
VAR TabelaGeneros =
    SUMMARIZE(
        vgsales, 
        vgsales[Genre],
        "TotalVendas", SUM(vgsales[Global_Sales])
    )
VAR TopGenero =
    TOPN(1, TabelaGeneros, [TotalVendas], DESC)
RETURN
    MAXX(TopGenero, vgsales[Genre])
# Exibe o gênero de jogo mais vendido
```

<hr>

<b>Cartão</b>

Exibe a plataforma de console mais vendida

Medida em DAX contida no Gráfico:

```python
Plataforma Mais Vendida = 
VAR TabelaPlataformas = 
    SUMMARIZE(
        vgsales, 
        vgsales[Platform],
        "TotalVendas", SUM(vgsales[Global_Sales])
    )
VAR TopPlataforma = 
    TOPN(1, TabelaPlataformas, [TotalVendas], DESC)
RETURN
    MAXX(TopPlataforma, vgsales[Platform])
#Exibe a plataforma de console mais vendida
```

<hr>

<b>Gráfico de Barras Empilhadas</b>

Exibe os jogos com maior volume de vendas.

Eixo Y: Name 

Eixo X: SUM (Global_Sales)

<hr>

<b>Gráfico de Barras Empilhadas</b>

Exibe as plataformas com maior volume de vendas.

Eixo Y: Platform

Eixo X: NA Sales, EU Sales, JP Sales, Other Sales

<hr>

<b>Gráfico de Linha</b>

Exibe as vendas totais por ano.

Eixo X: Year(Ano)

Eixo Y: Total Vendas Globais

Medida em DAX contida no gráfico:

```python
Total Vendas Globais = SUM(vgsales[Global_Sales])
#Exibe as Vendas Totais
```

<hr>

<b>Gráfico de colunas empilhadas</b>

Exibe as Vendas totais por Plataforma

Eixo X: Plataform

Eixo Y: Total Vendas Globais (Medida)

<hr>

Ainda na página atual de Visão Geral das Vendas, tem um botão para alternar as visualizações para Gênero do Jogo, mudando alguns gráficos.

Os gráficos presentes após a mudança são:

<b>Grafico de Colunas Empilhadas</b>

Exibe o Total de Vendas por Gênero

Eixo X: Genre

Eixo Y: Total Vendas Globais (Medida)

<hr>

<b>Gráfico de Barras Empilhadas</b>

Exibe as Vendas Totais por Gênero de Jogo

Eixo Y: Genre

Eixo X: JP Sales, NA Sales, EU Sales, Ohther Sales

<hr>

<b>Gráfico de Colunas Empilhadas</b>

Exibe o Rank por Gênero de Jogo

Eixo X: Genre

Eixo Y: Soma de Rank

<hr>

A página atual também conta com dois filtros. Podendo filtrar os gráficos por ano e por nome do Jogo. Os gráficos utilizados foram Segmentação de Dados.

<hr>

<h2>Análise por Desenvolvedora</h2>

Essa página traz análises gerais e detalhadas das Desenvolvedoras dos jogos

<hr>

<b>Gráfico de Barras Empilhadas</b>

Exibe as vendas totais por Desenvolvedoras.

Eixo Y: Publisher

Eixo X: Total Vendas Globais (Medida)

<hr>

<b>Tabela</b>

Exibe várias inoformações em um único Gráfico.

Colunas: Desenvolvedora, Jogo, Vendas Totais (Medida)

<hr>

<b>Gráfico de Dispersão</b>

Exibe a Quantidade de publicação de jogos por ano e as Vendas totais por ano.

Eixo X: Year(Ano)

Eixo Y: Contagem de Publisher

<hr>

<b>Cartão</b>

Exibe o Ano com mais Vendas

Medida DAX presente no gráfico:

```python
Ano Mais Vendas = 
VAR TabelaAnos = 
    SUMMARIZE(
        vgsales,
        vgsales[Year],
        "TotalVendas", SUM(vgsales[Global_Sales])
    )
VAR TopAno =
    TOPN(1, TabelaAnos, [TotalVendas], DESC)
RETURN
    MAXX(TopAno, vgsales[Year])
```

<hr>

<b>Cartão</b>

Exibe a Desenvolvedora com mais vendas.

Medida DAX presente no gráfico:

```python
Desenvolvedora Mais Vendida = 
VAR TabelaPublicadoras =
    SUMMARIZE(
        vgsales,
        vgsales[Publisher],
        "TotalVendas", SUM(vgsales[Global_Sales])
    )
VAR TopPublicadora =
    TOPN(1, TabelaPublicadoras, [TotalVendas], DESC)
RETURN
    MAXX(TopPublicadora, vgsales[Publisher])
```

<hr>

<h1>Considerações Técnicas</h1>

<h4><b>Fontes de Dados e Transformação</b></h4>

<hr>

<b>Origem dos Dados:</b> 

O arquivo vgsales.csv foi carregado direto no Power BI.

<b>Preparação dos Dados:</b> 

Foram realizadas transformações para corrigir tipos de dados, tratamento de valores nulos, extração de caracteres, transformação de caracteres, tratamento de vazios.

<b>Interatividade:</b>

Cada página possui filtros (slicers) que permitem ao usuário segmentar os dados por ano, plataforma, gênero ou desenvolvedora.
