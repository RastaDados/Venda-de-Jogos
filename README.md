<h1>Vendas Gerais do Mercado de Jogos</h1>

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

O relatório é dividido em três páginas contendo análises específicas.

<b>Visão Geral</b>

- Objetivo: Apresentar um panorama geral das vendas de videogames.

- Gráficos e Elementos contidos na página:

<b>Card – Total de Vendas Globais</b>

Medida DAX contida no gráfico:

```python
TotalVendasGlobais = SUM(vgsales[Global_Sales])
#Exibe a soma total de todas as vendas globais.
```

<hr>

<b>ard - Gênero de Jogo mais Vendido</b>

Exibe o Gênero de jogo mais vendido

Medida contida no Gráfico:

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

<b>Card - Plataforma de Console Mais vendido</b>

Exibe a plataforma de console mais vendida

Medida contida no Gráfico:

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

<b>Gráfico de Barras Empilhadas – Total de Vendas Por Nome do Jogo</b>

Exibe os jogos com maior volume de vendas.

Eixo Y: Name 

Eixo X: SUM (Global_Sales)

<hr>

<b>Gráfico de Barras Empilhadas - Venda de Plataformas por Região</b>

Exibe as plataformas com maior volume de vendas.

Eixo Y: Platform

Eixo X: NA Sales, EU Sales, JP Sales, Other Sales

<hr>

<b>Gráfico de Linha - Vendas Totais por Ano</b>



Gráfico de Pizza – Participação de Mercado por Plataforma

Demonstra o percentual de vendas de cada plataforma.

Fatias: Platform

Valores: SUM(Global_Sales)



3.2. Página: Análise por Plataforma
Objetivo: Comparar o desempenho das plataformas.
Gráficos e Elementos:
Gráfico de Linhas – Vendas por Ano e Plataforma:
Eixo X: Year
Eixo Y: SUM(Global_Sales)
Legenda: Platform
Explicação: Mostra a evolução de vendas para cada plataforma ao longo do tempo.

Gráfico de Barras Empilhadas – Vendas por Plataforma e Região:
Eixo Y: Platform
Valores: NA_Sales, EU_Sales, JP_Sales, Other_Sales
Explicação: Evidencia em quais regiões cada plataforma performa melhor.

Card – Plataforma Mais Vendida:
Medida DAX:

DAX
Copiar
Editar
PlataformaMaisVendida = 
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
Explicação: Identifica e exibe a plataforma com o maior volume de vendas globais.

3.3. Página: Análise por Gênero
Objetivo: Verificar quais gêneros de jogos são os mais lucrativos.
Gráficos e Elementos:
Gráfico de Colunas – Vendas por Gênero:
Eixo X: Genre
Eixo Y: SUM(Global_Sales)
Explicação: Compara o total de vendas entre os diferentes gêneros.

Gráfico de Barras Empilhadas – Vendas por Gênero e Região:
Eixo Y: Genre
Valores: NA_Sales, EU_Sales, JP_Sales, Other_Sales
Explicação: Analisa a distribuição de vendas dos gêneros por região.

Card – Gênero Mais Vendido:
Medida DAX:

DAX
Copiar
Editar
GeneroMaisVendido = 
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
Explicação: Retorna o gênero com o maior volume de vendas.

3.4. Página: Análise por Publicadora (Desenvolvedora)
Objetivo: Identificar a publicadora/desenvolvedora com maior volume de vendas.
Gráficos e Elementos:
Gráfico de Barras – Top 10 Publicadoras:
Eixo Y: Publisher (top 10)
Eixo X: SUM(Global_Sales)
Explicação: Exibe as publicadoras com maiores vendas.

Tabela – Jogos Mais Vendidos por Publicadora:
Colunas: Publisher, Name, Global_Sales
Explicação: Lista os jogos mais vendidos para cada publicadora.

Gráfico de Dispersão – Evolução das Publicadoras:
Eixo X: Year
Eixo Y: SUM(Global_Sales)
Legenda: Publisher
Explicação: Visualiza a performance das publicadoras ao longo dos anos.

Card – Publicadora Mais Vendida:
Medida DAX:

DAX
Copiar
Editar
PublicadoraMaisVendida = 
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
Explicação: Identifica e exibe a publicadora com o maior volume de vendas.

3.5. Página: Evolução Temporal
Objetivo: Analisar tendências de vendas ao longo dos anos.
Gráficos e Elementos:
Gráfico de Linhas – Vendas Globais ao Longo dos Anos:
Eixo X: Year
Eixo Y: SUM(Global_Sales)
Explicação: Exibe a evolução total do mercado de videogames.

Gráfico de Barras Empilhadas – Vendas por Ano e Gênero:
Eixo X: Year
Eixo Y: SUM(Global_Sales)
Pilha: Genre
Explicação: Permite visualizar como os diferentes gêneros evoluíram ao longo do tempo.

Card – Ano com Maior Venda:
Medida DAX:

DAX
Copiar
Editar
AnoMaisVendas = 
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
Explicação: Retorna o ano com o maior volume de vendas globais.

3.6. Página: Regiões de Venda
Objetivo: Comparar o desempenho de vendas em diferentes regiões.
Gráficos e Elementos:
Gráfico de Mapa – Vendas por Região:
Localização: Região (NA, EU, JP, Other)
Tamanho do marcador: SUM(Global_Sales)
Explicação: Demonstra a distribuição geográfica das vendas.

Gráfico de Barras – Top 10 Jogos por Região:
Eixo Y: Name
Eixo X: Vendas em cada região (NA_Sales, EU_Sales, etc.)
Explicação: Identifica os jogos mais vendidos em cada região.
