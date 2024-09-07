# 🎥MERCADO DE FILMES🎬
Uma análise de filmes lançados no perído de 1980 à 2020. Fazendo um levantamento de quanto eles lucraram, quais filmes mais fizeram bilheteria, qual estúdio lucrou mais, qual diretor foi mais lucrativo, qual filme teve maior índice de ganho e qual ator é o mais rentável.

Os dados foram obtidos no site Kaggle, feito por Daniel Grijalva.

Link do Dataset: https://www.kaggle.com/datasets/danielgrijalvas/movies
<br>
<br>
> [!NOTE]
> Este projeto possui como único propósito para estudo pessoal.<br>

## TECNOLOGIAS UTILIZADAS
- [Python 3.10](https://www.python.org/) (Linguagem de Programação)
- [Google Colab](https://colab.google/) (Editor de Código)
- [Pandas 2.2.2](https://pandas.pydata.org/) (Tratamento de dados)
- [Plotly 5.24.0](https://plotly.com/) (Visualização de dados)

## Importando Bibliotecas
```
import numpy as np
import pandas as pd
import plotly.express as px
import warnings
from plotly.offline import offline, iplot

warnings.filterwarnings('ignore')

pd.options.display.float_format = "{:,.1f}".format
```
## Acessando o Dataset
```
df = pd.read_csv('movies.csv', encoding='latin-1')
```
Usando o comando `df.head()` é possível ver as 5 primeiras linhas da tabela.

![tabela-dataset](https://github.com/user-attachments/assets/6df1d1f5-eba0-407f-92e2-6c6ec52201b4)

## Traduzindo os nomes das colunas
Para um melhor entendimento do que tratam os valores das colunas, decidi traduzir os nomes delas.
```
colunas = ['nome', 'classificação', 'gênero', 'ano', 'lançamento', 'nota', 'votos', 'diretor', 'roterista', 'estrela', 'país', 'orçamento', 'bilheteria', 'estúdio', 'duração']
df.columns = colunas
```
Chamando o comando `df.head()` a tabela fica assim:

![tabela-traduzido](https://github.com/user-attachments/assets/06b5ad3f-7be5-4752-9eff-7e516083ccb3)

## As classificações com mais filmes
Para verificar quais as faxas etárias que contém mais filmes, usei os seguintes comandos:
```
classificacao = df['classificação'].value_counts()
(classificacao/df.shape[0]*100).apply(lambda x: f'{x: 0.2f} %')
```
O que gerou o seguinte resultado:

![tabela-classificacoes](https://github.com/user-attachments/assets/79f03fbe-65ba-4cb5-ab4c-a0dbec87c752)

Já o gráfico ficou da seguinte forma:
![newplot](https://github.com/user-attachments/assets/0c9f7f9f-b4d2-41d6-ab95-434a80ffc2a3)
A classificação R, ou seja, filmes para maiores de 17 anos, nos Estados Unidos, o que seria no Brasil acima dos 18 anos, possui mais filmes produzidos.<br>
Isso pode ser refletido na quantidade de filmes de terror, mas, principalmente, dos filmes mais violentos do gênero de ação.

## Top 10 Maiores Bilheterias do Cinema
Com os seguintes comandos é possível classificar os filmes por bilheteria:
```
print('As 10 maiores bilheterias do cinema')
bil = df.sort_values(by='bilheteria', ascending=False, ignore_index=True)
top_bil = bil[['nome', 'bilheteria']]
```
E usando o comando `top_bil.head(10)` podemos visualizar como ficou a tabela:

![tabela-bilheteria](https://github.com/user-attachments/assets/b81fc116-1956-4f91-8bf4-2cf10e3634b3)

![newplot2](https://github.com/user-attachments/assets/f3144184-109b-4df5-a23d-68e7be21d13e)

## Top 10 Filmes mais bem avaliados

![tabela-avaliados](https://github.com/user-attachments/assets/da46d572-e683-4052-8cd6-1d09b3415150)

![grafico-avaliados](https://github.com/user-attachments/assets/e3203eba-50b7-4a2b-88b0-886fd65687df)

## Top 10 Gêneros mais rentáveis

![tabela-generos](https://github.com/user-attachments/assets/a884fb4a-45d2-4f7e-974d-9df6774c7721)

![grafico-generos](https://github.com/user-attachments/assets/ac4ec780-2186-42eb-81da-75c8c3512d3f)

## Top 10 Estrelas mais rentáveis

![tabela-ator](https://github.com/user-attachments/assets/23e93f93-a002-42a8-ad2c-d102d799cd6c)

![grafico-ator](https://github.com/user-attachments/assets/ee9d1385-7177-47df-8e60-4b5494f5997a)

## Top 10 Diretores mais rentáveis

![tabela-diretor](https://github.com/user-attachments/assets/53e74fbd-070c-4588-9e1b-2a24cfeda00a)

![grafico-diretor](https://github.com/user-attachments/assets/56995009-d0af-481f-ad61-4ebe3b86c52b)

## Top 10 Atores com mais filmes

![tabela-qtdfilmes](https://github.com/user-attachments/assets/0e1f158a-0818-4bbf-bad8-46b05a7ca4e1)

![grafico-qtdfilmes](https://github.com/user-attachments/assets/ec5c3811-68af-493d-9873-c00ed02d1b11)

## Top 10 Estúdio com maior bilheteria

![tabela-estudio](https://github.com/user-attachments/assets/94b6b28d-7f18-4248-98c9-4aa38404bcc8)

![grafico-estudio](https://github.com/user-attachments/assets/150aa7d9-fe77-4bf2-b455-5d077f6ae4f8)

## Relação Bilheteria x Orçamento
Para poder visualizar a relação entre quanto o filme custou e quanto ele lucrou, fiz o seguinte algoritmo:
```
fig = px.scatter(
    df,
    x = 'orçamento',
    y = 'bilheteria',
    trendline = 'ols',
    template = 'plotly_dark',
    color = 'bilheteria',
    color_discrete_sequence = ['#45FFCA'],
    title = 'Relação Bilheteria e Orçamento',
    labels = {'bilheteria': 'Bilheteria', 'orçamento': 'Orçamento', 'nome': 'Filme'},
    hover_name = 'nome',
    hover_data = ['bilheteria', 'orçamento']
    )
```
Chamando o comando `iplot(fig)`, temos o seguinte gráfico:

![grafico-bil_orc](https://github.com/user-attachments/assets/d0947c41-867f-41f1-8913-8de763879452)

## Top 10 Filmes com maior índice de lucro
Agora, para obter os maiores índices de orçamento, criei o seguinte algoritmo:
```
df['% lucro'] = (df['bilheteria'] / df['orçamento']) * 100
pontos_porcent = df[['nome', 'bilheteria', 'orçamento', '% lucro']].sort_values(by='% lucro', ascending=False, ignore_index=True)
```
Nela, criei uma nova tabela no Dataframe, que leva o percentual de lucro que cada filme obteve.
Com o comando `pontos_porcent.head(10)`, geramos a seguinte tabela:

![tabela-percentual](https://github.com/user-attachments/assets/b4b7c071-4647-49e3-a3d1-84f8178fbcd3)

Para obter o gráfico fiz o seguinte código:
```
top_dez = pontos_porcent.head(10)[::-1]
fig = px.bar(
    data_frame = top_dez,
    orientation = 'h',
    y = 'nome',
    x = '% lucro',
    color = '% lucro',

    labels = {'nome': 'Filme', '% lucro': 'Margem de Lucro (%)'},
    title = 'Top 10 Filmes mais rentáveis',
    text_auto = '.2s',
    template = 'plotly_dark',
    color_continuous_scale = ['#00FFAB', '#00FFAB', '#A084E8']
)
```
E dando o comando `iplot(fig)`, temos o resultado:

![grafico-percentual](https://github.com/user-attachments/assets/06a058ec-79bc-4def-853f-135172a6e3f1)

# CONCLUSÃO

## E O OSCAR 🎥🏆 DE ATOR COM MAIS FILMES VAI PARA...

![download](https://github.com/user-attachments/assets/62449333-8bcf-4fd3-9c89-2b0d28a9037b)

Com 40 filmes no currículo, Nicolas Cage é o ator que mais protagonizou filmes.

## E O OSCAR 🎥 🏆 DE FILME MAIS BEM AVALIADO VAI PARA...

![download](https://github.com/user-attachments/assets/21bace7a-61a1-44ff-a0c8-11b21bb420e6)

The Shawshank Redemption, ou "Um Sonho de Liberdade", em português, tem a nota mais alta da história, com 9,3 nas avaliações dos usuários no imdb.

## E O GÊNERO MAIS RENTÁVEL FOI...

![download](https://github.com/user-attachments/assets/3590e399-7130-4a4e-9d78-858cb856126b)

Os filmes do gênero de AÇÃO fizeram ao todo mais de 237 bilhões de dólares, sendo a principal aposta dos estúdios quando se quer lucrar na indústria.

## E O OSCAR 🎬 🏆 DE DIRETOR MAIS RENTÁVEL DA HISTÓRIA VAI PARA...

![download](https://github.com/user-attachments/assets/a9a82a0d-ee19-4a8b-95a7-32c8c24d60e1)

Steven Spielberg, somou mais de 9.6 bilhões de dólares com seus filmes, tornando-se o Diretor mais rentável da história.

## E O OSCAR 🎥🏆 DE FILME MAIS RENTÁVEL VAI PARA...

![download](https://github.com/user-attachments/assets/73aac2e8-f77f-4ef1-aa76-650aebdd5e9a)

Atividade Paranormal foi um fenômeno do gênero de Terror. Lançado em 2007, o filme contou com um orçamento de apenas 15 mil dólares, arrecadando mais de 193 milhôes em bilheteria. Tendo uma incrível marca de 1.289.038,7% de lucro.

## E O ESTÚDIO COM MAIOR BILHETERIA FOI...

![download](https://github.com/user-attachments/assets/e2c41cfc-c331-46eb-9001-82d5111121dd)

A WARNER BROS., somando as bilheterias de seus filmes, arrecadou mais de 54 bilhões de bilheteria, tornando-se o estúdio de cinema que mais lucrou na história.

## E O OSCAR 🎥🏆 DE ATOR MAIS RENTÁVEL VAI PARA...

![download](https://github.com/user-attachments/assets/a6721e38-0ae5-464e-b80d-a0b71b2d9f93)

Robert Downey Jr, mais famoso por seu papel como Tony Stark nos filmes da MARVEL, fez uma soma de quase 12 bilhões de dólares em bilheteria nos filmes que protagonizou. Muito devido ao sucesso de seu personagem na MARVEL, com a franquia Vingadores, cuja bilheteria foi a segunda maior da história, não conseguindo superar o maior fenômeno das bilheterias...

## E O OSCAR 🎥🏆 DE MAIOR BILHETERIA VAI PARA...

![download](https://github.com/user-attachments/assets/f5420cc3-eee0-4e3d-b2e1-e9d40c79661c)

Avatar, lançado em 2009, o fenômeno dirigido por James Cameron, faturou mais de 2,8 bilhões de dólares na bilheteria em todo o mundo, tornando-se a maior bilheteria de todos os tempos.
