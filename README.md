# Desafio Convenia

<!-- ![alt text](logo.jpg) -->

Este é um desafio proposto pela Convenia, com a finalidade de retirar insights de uma base de dados disponibilizada

## Base de Dados

A base de dados são duas planilhas:
>- celularessubtraidos_2024_1_6_(1)
>- celularessubtraidos_2024_7_9_(1)

Temos também a planilha *dicionario_bd_(1)* que explica melhor sobre as bases de dados, quais informações temos o que cada campo significa.

<br>

Com as bases disponibilizadas, utilizei o Python para poder realizar o primeiro tratamento de dados
___
### Python
Primeiramente, importei a biblioteca *Pandas* que será necessária para realizar a importação das planilhas e realizar os tratamentos dos dados.

````
import pandas as pd
````

Após a importação do *Pandas*, importei a primeira planilha e utilizei a função info() para poder verificar melhor os dados dessa primeira planilha, como nome das colunas, tipo de dados e quantos dados não nulos existentes:

````
celulares_subtraidos1 = pd.read_excel('celularessubtraidos_2024_1_6_(1).xlsb')
````

````
celulares_subtraidos1.info()
````

![alt text](image1.png)

Fiz o mesmo processo com a segunda planilha

````
celulares_subtraidos2 = pd.read_excel('celularessubtraidos_2024_7_9_(1).xlsb')
````

````
celulares_subtraidos2.info()
````

![alt text](image2.png)

Após o processo de importação das planilhas, realizei a união das duas planilhas, pois, as duas possuem a mesma estrutura de dados (mesma quantidade de colunas com o mesmo nome).

````
df = pd.concat([celulares_subtraidos1, celulares_subtraidos2])
`````

Agora temos um DataFrame com o nome de *df* que possui os dados das duas planilhas juntas.

![alt text](image3.png)

Algumas colunas apresentam valores nulos com tipo *object*. Para esses casos, irei utilizar a função *unique()* para poder visualizar os valores distintos em determinadas colunas.

Neste caso, irei realizar o mesmo processo abaixo nas colunas:
>- DESDOBRAMENTO
>- TIPO_INTOLERANCIA
>- DESCR_CONDUTA
>- DESCR_UNIDADE
>- CIRCUNSTANCIA
>- DESCR_TIPOLOCAL
>- DESCR_SUBTIPOLOCAL
>- FLAG_BLOQUEIO
>- FLAG_DESBLOQUEIO
>- DESCR_PERIODO

As demais colunas de Data, Hora ou Número, serão tratadas no Power BI.

````
df['TIPO_INTOLERANCIA'].unique()
````

No caso da coluna TIPO_INTOLERANCIA, temos os seguintes valores abaixo:

````
array([nan, 'Homofobia/Transfobia', 'Racial/Etnia/Cor'], dtype=object)
````

Como podemos visualizar, temos o valor *nan* que seriam os valores nulos, juntamento com outros dois valores preenchidos.

Para poder tratar os valores nulos, iremos utilizar a função *fillna()* que realizar o tratamento de todos os valores nulos dentro de determinado campo. No caso, iremos preencher dentro dessa função o valor *Não Informado* para que os valores nulos sejam alterados para esse valor.

````
df['TIPO_INTOLERANCIA'] = df['TIPO_INTOLERANCIA'].fillna('Não Informado')
````

Validando novamente a coluna, podemos verificar que todos os valores não nulos foram preenchidos, ficando da seguinte forma:

**Antes**: 
<br>
![alt text](images/image5.png)

**Depois** 
<br>
![alt text](images/image4.png)

Finalizado o processo de tratamento dos dados, iremos exportar os dados para um arquivo *celulares_subtraidos_consolidado* no qual iremos carregar no Power BI, finalizar o tratamento dos dados e realizar a construção dos painéis.


````
df.to_excel('celulares_subtraidos_consolidado.xlsx')
````




## Power BI
Após a es