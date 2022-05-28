Shell Sort 🐚
======

Concha o que?
---------

![shell](shell.jpg)

Como o nome já sugere, o **Shell Sort** é um algoritmo computacional de **ordenação**, ou seja, ele serve para solucionar o problema de ordenação de alguma lista de elementos que **não** estão em ordem. Como vimos em aula, cada algoritmo de ordenação tem suas **vantagens e desvantagens**. Nesse handout iremos entender em quais **situações** o *Shell Sort* é um algoritmo interessante de ser utilizado e como que ele funciona. 

Insertion Sort
---------
  
Ainda antes de começar a introdução do algoritmo *Shell Sort* propriamente dito, vamos fazer uma breve revisão do *Insertion Sort*. *Insertion Sort*? Não entendi. Calma aí jovem, tudo vai se esclarecer em seu devido momento.

??? Revisão

Reveja o **pseudocódigo** abaixo para entender a **lógica** do *Insertion Sort*:

 - A **“parte ordenada”** é o intervalo de 0 a i-1 e o **“resto”** é o intervalo de i a n-1.

 - O elemento “tirado” do “resto” é **sempre o primeiro**, ou seja, v[i].

```md
para todo i de 1 a n-1
    temp = v[i]
    encontre um índice j entre 0 e i-1 para "inserir" temp, sem estragar a ordenação
    desloque todos os elementos entre j e i-1 para a direita, sobrescrevendo v[i]
    v[j] = temp
```

Utilize a **animação** abaixo para simular o **funcionamento** do *Insertion Sort*:

:insertion

Assim podemos entender que a **ideia** por trás do *Insertion Sort*:

Dividir o vetor em uma **“parte ordenada**”, que começa vazia, e um **“resto”**, que começa com todos os elementos do vetor original. **Em cada iteração**, “tira” um elemento do “resto” e “insere” na “parte ordenada”, de forma que ela **continue ordenada**.

Caso tenha interesse, abaixo se encontra o **código** da implementação do *Insertion Sort*:

``` c
void insertion_sort(int v[], int n) {
    for (int i = 1; i < n; i++) {
        int temp = v[i];
        for(int j = i; j > 0 && v[j - 1] > temp; j--) {
            v[j] = v[j - 1];
        }
        v[j] = temp;
    }
}
```

???

??? Checkpoint

Tendo revisado o funcionamento do *Insertion Sort*, considere as listas abaixo:

``` c
int v1[] = {4, 8, 6, 7, 5}
int v2[] = {5, 3, 4, 2, 1}
```

Simule o algoritmo de ordenação *Insertion Sort* para cada uma das listas, escrevendo o estado da lista no **FINAL** de cada iteração do loop **EXTERNO**.

::: Gabarito
```
Lista v1:

4 8 6 7 5
4 6 8 7 5
4 6 7 8 5
4 5 6 7 8

Lista v2:

3 5 4 2 1
3 4 5 2 1
2 3 4 5 1
1 2 3 4 5
```
:::

Observem as ordenações realizadas por *Insertion Sort* acima. Pensem com calma, considerando tantos os loops externos quanto internos e respondam em qual delas que o algoritmo **performou bem** e em qual delas que o algoritmo teve que **realizar bem mais deslocamentos** para conseguir que o vetor esteja **finalmente ordenado**? Você é capaz de definir a **situação** na qual o *Insertion Sort* é um algoritmo que **não performa tão bem?** 

::: Gabarito

A lista v2 precisou de muito mais deslocamentos para que ficasse ordenada, diferentemente da lista v1. O que podemos observar é que no caso da lista v2, temos **elementos pequenos posicionados à direita do vetor**, o que força o algoritmo *Insertion Sort* a realizar muito mais iterações, consumindo mais tempo, do que no caso desses elementos já estarem mais ordenados, próximos do começo. 

:::

???

Shell Sort
---------

Finalmente meus colegas programadores! Vamos começar a aprender o *Shell Sort* propriamente dito. Mas espera aí... Na verdade já temos uma boa noção de como esse algoritmo funciona! (Uai?) Isso porque o *Shell Sort* nada mais é do que uma **melhoria do algortimo de ordenação *Insertion Sort***. 

Como entendemos na atividade acima, quando temos uma lista cujos **elementos menores estão muito à direita**, precisaremos de **mais iterações** para conseguir ordenar essa lista com o *Insertion Sort*.

Ok, entedemos qual é a situação na qual o *Insertion Sort* não performa tão bem, mas e se ao invés de pegarmos o elemento **adjacente**, como seria se o **intervalo entre os números fosse maior?**

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

Complexidade de tempo do Shell Sort
---------

O *Shell Sort* é um algoritimo extremamente utilizado quando uma recursão **excede o limite** ou quando o uso do *Insertion Sort* por conta de **números próximos estarem muito afastados um do outro** seria equivocado, pois o *Shell Sort* faria uma menor quantidade de trocas para conseguir ordenar o array.

??? Checkpoint

A partir do conhecimento obtido durante este e handout, sabendo que o *Shell Sort* é um algoritmo pensado para ser uma **melhoria** do *Insertion Sort* nas situações em que o mesmo **não performaria bem**, realizando ordenações em gaps e por fim um próprio *Insertion Sort* (quando gap = 1), reflita: 

Qual seria a **complexidade do pior caso** do *Shell Sort*? Será que dependendo do caso, o pior caso do *Shell Sort* pode ser pior do que o pior caso do *Insertion Sort*?

::: Gabarito
Mesmo com tudo que o *Shell Sort* faz a mais que o *Insertion Sort*, seu **pior caso continua sendo quadrático**, assim como o próprio *Insertion Sort*, afinal se é uma melhoria do algoritmo, não faria sentido que sua complexidade fosse pior. Na pratica, espera-se que o *Insertion Sort* final seja mais rapido pois o vetor ja esta mais ordenado que antes.
:::

???

| Melhor      | Media        | Pior |         
| :---        |    :----:    |---:  |
|O(n* log n)  | O(n* log n)  |O(n^2)|

A **complexidade de tempo** do algoritimo varia de acordo com a **sequência de incremento escolhida** (gap), sendo a melhor sequência de incremento **desconhecida**.

Em seu **melhor caso**, a complexidade do algoritimo fica O(n * log n), esse caso ocorre quando o array **já está ordenado** o número de comparações para cada incremento é **igual ao tamanho do array**.

??? Checkpoint
Para finalizar este handout, vamos pensar em uma última questão. A partir dos conceitos apresentados acima, por que é difícil chegar em uma **sequência de gaps ideal**? 

**Dica**, pense sobre o que aconteceria se utilizassemos **poucos gaps** além do gap = 1 e se utilizassemos **gaps de modo exagerado**.

::: Gabarito
A dificuldade em se encontrar uma **sequência de gaps ideal**, se dá pela questão de não sabermos exatamente se estamos **utilizando gaps de mais ou de menos**. Caso sejam usados **poucos gaps** alem do gap = 1, iremos **preordenar menos o vetor** antes do insertion sort. Já se realizarmos o *Shell Sort* com **muitos gaps** antes de chegar no gap = 1, vamos ter um **vetor bem ordenado** quando chegar ao insertion sort, mas até chegar nele podemos **consumir muito tempo**, piorando a situação
:::

???