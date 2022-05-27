Parte do Paulo
======

Usando a mesma lógica do *insertion sort*, vamos descartar a ideia de usar os elementos adjacentes do vetor. Ao invés disso, vamos colocar um intervalo entre os elementos a serem comparados.

A comparação e o deslocamento dos menores elementos para esquerda era da seguinte maneira:

![](insertion_sort.png)

Ao invés de compararmos o 1 com 7, vamos pular uns indíces e compará-lo com o 2. Esse número de índices que pulamos, ou intervalo, é connhecido como **gap**:

![](shellsort_1_gap.png)

Ou seja, a idéia aqui é você comparar o elemento atual com um outro "mais longe", a um gap de distância, em seguida, realizamos a lógica do insertion.


Okay, mas no que isso vai ajudar? Inicialmente, parece até um pouco estranho fazer isso, mas essa lógica é a chave para combater uma das fraquezas do *insertion sort*: quanto mais pra direita estiver um número pequeno, mais deslocamentos ele precisa fazer para a esquerda. Ou seja, o *insertion* trabalha **bem** com vetores que possuem um certo nível de ordenância, caso o contrário, ele se dá mal.Um pouco confuso? Tudo bem, vamos explorar essa idéia um pouco mais pra frente, por isso, vamos focar primeiro no funcionamento do algoritimo. 

Vamos facilitar nossa vizualização. Dado o vetor abaixo, vamos imaginar um par de subvetor para cada comparação feita com um gap igual a 2. 


![](vetor_1.png)

Ficaria algo parecido como abaixo.

![](gabarito_check_1.png)

Note que {red}(não) foi realizado as trocas dos elementos, só fizemos a separação dos conjuntos, que ficaram da seguinte maneira:

```
{33, 40}
{31,  8}
{40, 12}
{8,  17}
{12, 25}
{17, 42}
```

Vamos ver se você entendeu a lógica. 

??? Checkpoint 1
Dado o vetor abaixo, separe-o em subconjuntos, considerando um gap igual a 2.

![](vetor_check_1.png)
::: Gabarito
```
{44, 20}
{2,  15}
{20, 45}
{15, 14}
{45, 25}
{14, 42}
```
:::
???

??? Checkpoint 1.1
Dado o vetor abaixo, separe-o em subconjuntos, considerando um gap igual a 3.

![](vetor_check_1_1.png)

::: Gabarito
```
{22, 62}
{16, 15}
{60, 20}
{62,  7}
{15,  4}
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
{46, 93}
{38, 82}
```
:::
???

Até aqui, o conceito de subvetor deve ter fica mais claro. Vamos voltar com o vetor do ``Checkpoint_1``, que está logo abaixo. Realizaremos a lógica do *insertion sort* para cada um dos cojuntos de subvetores.

![](gabarito_check_1.png)

**obs:** Lembre que se o próximo elemento for menor que o primeiro, troca, senão, faz nada. Recomendo fazer no papel ou tablet.


```
{33, 40}
{8,  31}
{12, 40}
{17, 31}
{25, 40}
{31, 42}
```


Assim, ficamos com o vetor ordenado da maneira abaixo. Simples, certo? E é assim que o *shell sort* funciona.

![](vetor_2.png)

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

Pera lá, a verdade é que fizemos isso pra facilitar o entendimento do algoritimo. Então vamos fazer o *shell sort* de verdade, agora seguindo as regras descritas acima.

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
Seguindo a sequência adotada do gap, vamos dividí-lo por 2. Realize a ordenação do vetor adquirido no exercício anterior, só que agora, com o gap = 2. 

::: Gabarito
![](gabarito_check_4.png)

Dessa maneira, o vetor ficará ordenado da seguinte maneira:

![](gabarito_check_4_2.png)

:::

???

Antes de partir para a última etapa quando gap é igual a 1, por acaso não ficou uma pulga atrás da orelha quando a gente faz um *shell sort* de gap igual a 1? Pense bem, se estamos comparando o elemento atual com o próximo a uma distância igual a 1, basicamente estamos comparando o elemento adjacente! Isso soa familiar? Sim, é a mesma coisa do que fazer um *insertion sort*! Nesse caso em particular, não só vamos usar a lógica do *insertion*, mas como também estaremos realizando um *insertion sort* na prática. 

Com isso em mente, vamos realizar a última etapa da ordenação deste vetor!

??? Checkpoint 5
Realize a última etapa de ordenação do vetor, com um gap = 1, ou seja, um *insertion sort*!

::: Gabarito
![](gabarito_check_5.png)

:::

???


