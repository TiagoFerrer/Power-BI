# DASHBOARD COMERCIAL
Este painel de controle foi criado a partir dos cursos da DSA sobre Microsoft Power BI, abrangendo áreas de Business Intelligence e Data Science. Os conjuntos de dados empregados foram disponibilizados diretamente pelo conteúdo programático do curso. 
## Objetivo
O propósito é fornecer uma representação visual nítida e intuitiva dos dados, gerando percepções valiosas para embasar decisões e proporcionar uma experiência eficaz e impactante na análise dos dados.
Algumas das perguntas abordadas incluem:
1. Qual o total de vendas, o lucro, a quantidade de vendas realizadas e o valor total de comissão pagos?
2. Como são as vendas por categoria, por segmento e por fabricante?
3. Como os dados de venda se comportam por ano, com comparativo ao ano anterior? 
4. Qual o total de comissão paga, por vendedor, quem são os maiores vendedores?
5. Quais são os cinco maiores vendedores, por cada um dos segmentos?
6. Qual a representatividade de cada categoria de produtos, em relação à quantidade, custo, lucro e total de vendas?
7. Qual o total de vendas por cidade?

## Descrição dos dados
| Coluna  |Descrição |
| :------------- |:-------------|
| ID-Produto      | Identificação do produto     |
| Produto      | Descrição do produto     |
| Categoria      | Categoria que pertence o produto     |
| Segmento      | Segmento do produto     |
| Fabricante      | Fabricante do produto     |
| Loja      | Código da loja    |
| Cidade      | Cidade da loja     |
| Estado      | Estado da loja     |
| Vendedor      | Nome do vendedor     |
| ID-Vendedor      | Identificação do vendedor     |
| Comissão (Percentual)      | Comissão do vendedor em relação a venda. Valor percentual     |
| Data Venda      | Data que foi feita a venda     |
| ValorVenda      | Valor da venda     |
| Custo      | Custo do produto     |

## Tratamento dos Dados
Os dados foram extraídos do arquivo "Dados_Comerciais.xlsx", originalmente armazenados em uma única tabela. Notavelmente, a base de dados não apresentava valores nulos, em branco ou outliers, dispensando, assim, a necessidade de proceder a uma limpeza de dados. Algumas transformações foram implementadas, incluindo a conversão do tipo de dado "ID-Vendedor" de numérico para texto, bem como a definição do campo "Date" como formato de data.
Ademais, uma transformação crucial foi realizada para estruturar as tabelas Dimensão e Fato. Essas transformações resultaram nas seguintes tabelas:

* DimLojas: Incorporando os atributos de Loja, Cidade e Estado.
* DimProdutos: Abraçando ID-Produto, Produto, Categoria, Segmento, Fabricante e Custo.
* DimVendedor: Englobando ID-Vendedor e Vendedor.
FactVendas: Compreendendo ID-Produto, Loja, ID-Vendedor, ValorVenda, Data e Comissão (Percentual).

No contexto da tabela "FactVendas", destaca-se a gênese da coluna "Comissão". Essa coluna é calculada pela multiplicação do "ValorVenda" pelo valor correspondente em "Comissão (Percentual)", dividido por 100.
Além disso, diversas métricas suplementares foram engendradas para enriquecer a visualização de dados e otimizar a disposição dos cartões no dashboard.

## Visão geral
### Filtros
Para  aprimorar a análise de dados, permitindo aos usuários ajustar critérios de visualização, personalizar a exploração de dados e identificar insights cruciais, cada uma das abas possuem filtros estratégicos. Essa interatividade direcionada potencializa decisões informadas em diversas áreas, promovendo uma análise mais profunda e estratégica para orientar o sucesso da organização.
**Data** - Seleciona a data inicial e final
**Ano** - Seleciona o ano a ser analisado
**Segmento** - Pode escolher entre os três segmentos dos dados.
**Categoria** -  Pode selecionar, dentre as cinco categorias, as que deseja analisar.
**Fabricante** - Onde pode ser selecionado o fabricante.

### Painéis e Insights do Dashboard
#### Visão Geral:
Os dados aqui apresentados refletem o conjunto completo de informações, sem a aplicação de filtros específicos. O filtro de data abrange o período total selecionado. No módulo de "Vendas Anuais", o ano-base padrão é 2015, o último ano disponível nos registros.
#### Performance de Vendas:
A primeira tela do dashboard proporciona um panorama abrangente das métricas vitais de vendas. O gráfico de pizza "Vendas por Segmento" oferece uma análise segmentada das vendas. O gráfico de barras horizontais "Vendas por Categoria" permite uma análise hierárquica das categorias de vendas. O gráfico de barras "Vendas por Fabricante" apresenta os valores e percentuais de vendas atribuídos a cada fabricante.
#### Vendas Anuais:
Nesta tela, o foco recai sobre uma análise anual das vendas. Os cartões iniciais exibem os totais de vendas, lucro e quantidade de vendas. Além dos dados do ano selecionado, destacam-se as variações percentuais em relação ao ano anterior e o mês com melhor resultado. O custo anual é detalhado em um cartão adicional, fornecendo não apenas a variação percentual em relação ao ano anterior, mas também o percentual de custo. Três gráficos de barras complementares apresentam dados de lucro, quantidade de vendas e vendas por mês, possibilitando uma comparação entre o ano selecionado e o anterior.
#### Desempenho dos Vendedores:
Nesta tela, é possível explorar a comissão total de cada vendedor, identificar os cinco principais vendedores em termos de vendas totais, bem como os cinco principais vendedores em cada segmento.
#### Análise de Produtos:
A tela "Análise de Produtos" oferece uma análise categorizada da quantidade, custo total, total de vendas e lucro total por produto em cada categoria.
#### Mapa de Vendas:
Este mapa interativo apresenta dados de total de vendas, lucro e quantidade de vendas por cidade onde as lojas estão localizadas.
### Resultados:
O dashboard fornece insights valiosos sobre as vendas do cliente, destacando:
* **Variações Anuais**: Observa-se uma queda acentuada de mais de 30% nas vendas de 2014 em relação a 2013, destacando-se como o segundo pior ano após o início da análise em 2012. No entanto, o ano de 2015 registrou um aumento notável de mais de 160% em todas as métricas.
* **Padrões de Vendas**: A análise revela que as vendas não são sazonais, embora novembro se destaque como o mês de maior atividade.
* **Segmentos e Categorias**: O segmento doméstico é o principal destino das vendas, representando 70% das transações. Dentre as categorias, os Eletrodomésticos contribuem significativamente, representando 50% das vendas.
* **Desempenho de Vendedores**: André Pereira lidera em vendas, enquanto Maria Fernandes se destaca com ótimas vendas em todos os segmentos, estabelecendo-se como a segunda melhor vendedora geral.
* **Distribuição de Categoria**: Os Eletrodomésticos dominam, contribuindo com cerca de 50% nas métricas de categoria, quantidade de produtos, custo, vendas totais e lucro. Os Celulares representam cerca de 10% nas métricas de quantidade de produtos e custos, mas geram 31% do lucro e 27% das unidades vendidas. Já os Eletroportáteis contribuem com 25% nas métricas de quantidade de produtos e custos, correspondendo a 5% das vendas totais e 1% do lucro.
* **Vendas por Localização**: As lojas de São Paulo lideram as vendas, seguidas pelas lojas do Rio de Janeiro e Belo Horizonte.

Este dashboard oferece análises profundas das vendas, fornecendo valiosos insights para aprimorar a estratégia de negócios.
