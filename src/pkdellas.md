Parte do Paulo
======

A comparação e o deslocamento dos menores elementos para esquerda era da seguinte maneira:

![](insertion_sort.png)

Ao invés de compararmos o 1 com 7, vamos pular uns indíces e compará-lo com o 2. Esse número de índices que pulamos, ou intervalo, é connhecido como **gap**:

![](shellsort_1_gap.png)

Ou seja, a idéia aqui é você comparar o elemento atual com um outro "mais longe" a um gap de distância, e em seguida, realizar a troca.

Conseguem exergar a vantagem aqui? Preste atenção no número 1. No *insetion*, ele vai da **sétima** posição para a **sexta** em 1 iteração. Mas na segunda lógica, ele foi da **sétima** posição para a **quarta** posição, em 1 iteração também! Se o nosso objetivo é ordenar, a segunda opção parece ser menos custosa em operação...bom, senhoras e senhores, eis o *shell sort*. Mas isso só é a ponta do iceberg, vamos nos aprofundar.

Para facilitar a nossa vizualização, utilizaremos o vetor abaixo. Vamos imaginar um par de subvetor para cada comparação feita com um gap igual a 2. 

![](vetor_1.png)

Ficaria algo parecido como abaixo.

![](gabarito_check_1.png)

Note que {red}(não) foi realizado as trocas dos elementos, só fizemos a separação dos conjuntos, que ficaram da seguinte maneira:

```
{33, 40, 12, 25}
{31, 8, 17, 42}
```

**OBS**: Não são apenas esses dois subvetores presentes no gap = 2, se continuássemos, haveria mais pares como:

```
{40, 12, 25}
{8, 17, 42}
{12, 25}
{17,42}
```
já que o algoritmo do *shell sort* "anda" ao longo do vetor até o limite do gap chegar no último índice. Mas para não deixar o desenho poluído, pegamos apenas os dois primeiros. 

Vamos ver se você entendeu a lógica. 

??? Checkpoint 1
Dado o vetor abaixo, separe-o em subconjuntos, considerando um gap igual a 2.

![](vetor_check_1.png)
::: Gabarito
```
{44, 20, 45, 25}
{2, 15, 14, 42}
```
:::
???

??? Checkpoint 1.1
Dado o vetor abaixo, separe-o em subconjuntos, considerando um gap igual a 3.

![](vetor_check_1_1.png)

::: Gabarito
```
{22, 62, 7}
{16, 15, 4}
```
:::
???

??? Checkpoint 1.2
Dado o vetor abaixo, separe-o em subconjuntos, considerando um gap igual a 4.

![](vetor_check_1_2.png)

::: Gabarito
```
{32, 39}
{27, 49}
```
:::
???

Até aqui, o conceito de subvetor deve ter fica mais claro. Vamos voltar com o vetor inicial, que está logo abaixo. Realizaremos a troca para cada um dos cojuntos de subvetores.

![](gabarito_check_1.png)

**obs:** Lembre que se o próximo elemento for menor que o primeiro, troca, senão, faz nada. Recomendo fazer no papel ou tablet.


```
{33, 12, 25, 40}
{8, 17, 31, 42}
```
Agora junte os dois subvetores para formarmos o vetor completo. Assim, ficaremos com o vetor ordenado da maneira abaixo. Simples, certo? E é assim que o *shell sort* funciona.

![](vetor_2.png)

Vamos ver se você entendeu até aqui.

??? Checkpoint 3
Realize a ordenação do vetor abaixo, só que agora, com o gap = 4. 

![](vetor_1.png)

::: Gabarito
![](gabarito_check_3.png)

Dessa maneira, o vetor ficará ordenado da seguinte maneira:

![](gabarito_check_3_2.png)

:::

???

??? Checkpoint 4
Utilizando o vetor adquirido no *Checkpoint 3*, realize a ordenação, só que agora, com o gap = 2. 

::: Gabarito
![](gabarito_check_4.png)

Dessa maneira, o vetor ficará ordenado da seguinte maneira:

![](gabarito_check_4_2.png)

:::

???

Vamos dar uma pausa nos exercícios e discutir. A essa altura do campeonato, pode ser que você teve alguns desses questionamento ao longo do handout:

1. Como eu decido meu gap? 

2. O gap sempre muda para cada iteração? Isso não fará com que eu pule alguns elementos para sempre?

Para aqueles que não se perguntaram isso, vamos esclarecer uma vez por todas as regras do *shell sort*.

O gap inicialmente começa com um valor referente ao vetor. No nosso caso, adotamos o gap inical como a metade do tamanho do vetor, ou seja, 

$$ gap = \frac{n}{2}$$

Logo, seguindo a lógica dessa sequência, o gap ficará assim:


$$ gap = \frac{n}{2}, \frac{n}{4}, \frac{n}{8}, . . . $$

e isso continua até o *gap ser igual a 1*.

Ué, mas a gente não adotou o gap incialmente a 2? E o tamanho do vetor é 8...algo de errado não está certo!

Pera lá, a verdade é que fizemos isso pra facilitar o entendimento do algoritimo. Mas de agora em diante, você deve realizar o *shell sort* seguindo as regras descritas acima.

Seguindo a sequência do gap nos últimos 2 exercícios, vamos fazer com ele igual a 1.

??? Checkpoint 5
Realize a ordenação do vetor com um gap = 1

::: Gabarito
![](gabarito_check_5.png)

:::

???

Por acaso você não ficou uma pulga atrás da orelha quando a gente faz essa etapa com gap igual a 1? Pense bem, se estamos comparando o elemento atual com o próximo a uma distância igual a 1, basicamente estamos comparando o elemento adjacente! Isso é a mesma coisa do que fazer um *insertion sort*! 

![](wtf.png)

Não faça essa cara, querido leitor. Eu sei que soa estranho isso...queríamos resolver a fraqueza do *insertion sort* usando a lógica do *shell sort*, mas no final das contas a gente acabou usando o *insertion* de novo. Mas a verdade é que isso faz todo o sentido! 

Se vocês lembrarem das aulas do *insertion sort*, vimos que ele tende a ter uma boa performance quando o vetor já possui um certo nível de ordenância, caso o contrário, a operação acaba ficando custosa. Isso significa que o *shell* na verdade combate esse problema, deixando o vetor parcialmente ordenado nas primeiras iterações para que no fim, o *insertion sort* finalize a ordenação total!

![](i-got-you.jpg)




