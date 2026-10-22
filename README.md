# Onde abrir 4 novas cafeterias em Chicago?

Análise geoespacial que usa a localização das bibliotecas públicas de Chicago como uma aproximação de áreas frequentadas por estudantes, leitores e pessoas que trabalham remotamente. O objetivo é comparar possíveis regiões para quatro novas cafeterias — não afirmar, apenas com esses dados, onde há maior demanda ou potencial de vendas.

[![Abrir no Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/alexandrescruz/analise-cafeterias-chicago/blob/main/Analise_cafeterias_chicago.ipynb)

## Pergunta e hipótese

**Pergunta de negócio:** quais regiões de Chicago podem ser consideradas para abrir quatro novas cafeterias?

**Hipótese:** regiões próximas a concentrações de bibliotecas públicas podem ser bons pontos de partida para investigar locais para as novas lojas.

## Análise

O notebook [`Analise_cafeterias_chicago.ipynb`](./Analise_cafeterias_chicago.ipynb):

1. coleta nomes e coordenadas das bibliotecas pela API de dados abertos da Prefeitura de Chicago;
2. remove coordenadas duplicadas e verifica se estão dentro de limites geográficos aproximados da cidade;
3. converte latitude e longitude para uma projeção local em quilômetros, adequada para calcular distâncias nessa escala;
4. agrupa as bibliotecas em quatro regiões usando **K-Means** e avalia os grupos com o método do cotovelo e o coeficiente de silhueta;
5. compara, em cada região, o centroide do grupo com a biblioteca que tem mais outras bibliotecas em um raio de 2 km;
6. apresenta os grupos e os candidatos em um mapa interativo.

## Principais resultados

- Na execução registrada no notebook, foram analisadas **82 bibliotecas**.
- O coeficiente de silhueta para quatro grupos foi **0,35**. A separação é moderada: os grupos devem ser entendidos como regiões de atendimento definidas para a análise, não como divisões naturais e bem isoladas da cidade.
- Os centroides servem como referências geográficas, mas podem não corresponder a um endereço comercial viável. Os pontos de maior densidade ficam em locais reais de bibliotecas, mas ainda precisam ser avaliados como possíveis endereços para uma cafeteria.

Os dados são consultados diretamente na API; portanto, a quantidade de registros e os resultados podem mudar em execuções futuras.

## Como executar

### Google Colab

Abra o notebook pelo botão no início deste README e execute as células em ordem. A primeira célula instala o Folium; as demais consultam a API da cidade.

### Localmente

Com Python e Jupyter Notebook instalados, instale as dependências e abra o notebook:

```bash
pip install requests pandas numpy scikit-learn matplotlib folium jupyter
jupyter notebook Analise_cafeterias_chicago.ipynb
```

É necessária uma conexão com a internet para consultar a API de dados abertos de Chicago.

## Dados

- **Fonte:** [Chicago Data Portal — Libraries: Locations & Hours](https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Libraries-Locations-and-Hours/x8fc-8rcq)
- **API consultada:** `https://data.cityofchicago.org/api/views/x8fc-8rcq/rows.json?accessType=DOWNLOAD`

## Ferramentas

Python, Requests, pandas, NumPy, scikit-learn, Matplotlib e Folium.

## Limitações e próximos passos

A proximidade de bibliotecas é apenas uma hipótese de demanda: não considera diretamente concorrência, fluxo de pessoas, perfil demográfico, aluguel ou vendas. Para apoiar uma decisão comercial, a análise pode ser complementada com dados sobre cafeterias existentes, população, universidades, escritórios, transporte público, visitas às bibliotecas e custos de aluguel.

Projeto desenvolvido durante o **IBM Data Science Professional Certificate**, na Coursera.
