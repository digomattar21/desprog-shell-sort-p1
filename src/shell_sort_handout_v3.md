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

Agora vamos praticar um pouco. Tendo revisado o funcionamento do *Insertion Sort*, veja as listas abaixo:

``` c
int v1[] = {4, 8, 5, 6, 7}
int v2[] = {5, 3, 2, 4, 1}
```

Considere essas mesmas listas logo antes do **último** loop **EXTERNO** do *Insertion Sort*:

``` c
int v1[] = {4, 5, 6, 8, 7}
int v2[] = {2, 3, 4, 5, 1}
```

Simule o algoritmo de ordenação *Insertion Sort* para cada uma das listas, escrevendo o estado da lista no **FINAL** de cada iteração do loop **INTERNO**, simulando apenas o **último** loop **EXTERNO** de modo completo.

::: Gabarito
```
Lista v1:

temp = [7]

4 5 6 8 8
4 5 6 7 8

Lista v2:

temp = [1]

2 3 4 5 5
2 3 4 4 5
2 3 3 4 5
2 2 3 4 5
1 2 3 4 5

```
:::

???

??? Checkpoint

Observem as ordenações realizadas por *Insertion Sort* acima. Pensem com calma considerando os dois casos e respondam em qual deles que o algoritmo **performou bem** e em qual delas que o algoritmo teve que **realizar bem mais deslocamentos** para conseguir que o vetor esteja **finalmente ordenado**. Você é capaz de definir a **situação** na qual o *Insertion Sort* é um algoritmo que **não performa tão bem?** 

::: Gabarito

A lista v2 precisou de muito mais deslocamentos para que ficasse ordenada, diferentemente da lista v1. O que podemos observar é que no caso da lista v2, temos a presença de **elementos pequenos posicionados à direita do vetor**, o que força o algoritmo *Insertion Sort* a realizar muito mais iterações, consumindo mais tempo do que no caso desses elementos já estarem mais ordenados, próximos do começo. 

:::

???

Shell Sort
---------

Finalmente meus colegas programadores! Vamos começar a aprender o *Shell Sort* propriamente dito. Mas espera aí... Na verdade já temos uma boa noção de como esse algoritmo funciona! (Uai?) Isso porque o *Shell Sort* nada mais é do que uma **melhoria do algortimo de ordenação *Insertion Sort***. 

Como entendemos na atividade acima, quando temos uma lista cujos **elementos menores estão muito à direita**, precisaremos de **mais iterações** para conseguir ordenar essa lista com o *Insertion Sort*.

Ok, entedemos qual é a situação na qual o *Insertion Sort* não performa tão bem, mas e se ao invés de pegarmos o elemento **adjacente**, como seria se o **intervalo entre os números fosse maior?**

A comparação e o deslocamento dos menores elementos para esquerda era da seguinte maneira:

![](insertion_sort.png)

Ao invés de compararmos o 1 com 7, vamos pular uns indíces e compará-lo com o 2. Esse número de índices que pulamos, ou intervalo, é conhecido como **gap**:

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
{60, 20}
{62, 7}
{15, 4}
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

Complexidade de tempo do Shell Sort
---------

O *Shell Sort* é um algoritimo extremamente utilizado quando uma recursão **excede o limite** ou quando o uso do *Insertion Sort* por conta de **números próximos estarem muito afastados um do outro** seria equivocado, pois o *Shell Sort* faria uma menor quantidade de trocas para conseguir ordenar o array.

??? Checkpoint

Considere o **pseudocódigo** abaixo para entender a **lógica** do *Shell Sort*:

```md
para todo gap
  para todo i de gap a n-1
    temp = v[i]
    considerando os índices i, i-gap, i-2*gap, i-3*gap,...
    encontre um índice j para "inserir" temp, sem estragar a ordenação
    desloque todos os elementos entre j e i-gap para a direita, sobrescrevendo v[i]
    v[j] = temp
```

Caso tenha interesse, abaixo se encontra o **código** da implementação do *Shell Sort*:

``` c
void shellSort (int v[], int n) {
  // Rearrange elements at each n/2, n/4, n/8, ... gaps
  for (int gap = n / 2; gap > 0; gap /= 2) {
    for (int i = gap; i < n; i++) {
      int temp = v[i];
      for (int j = i; j >= gap && v[j - gap] > temp; j -= gap) {
        v[j] = v[j - gap];
      }
      v[j] = temp;
    }
  }
}
```

Tendo em vista o funcionamento do *Shell Sort*, obtenha a **complexidade aproximada** para cada **gap** do algoritmo.

::: Gabarito

Para cada **gap** teremos:
- loop externo -> n - **gap** iterações

Para cada iteração do loop externo teremos:
- loop interno -> n/**gap** iterações

Desse modo, para cada um dos **gaps** teremos um loop de **complexidade** aproximada (n - **gap**) * (n/**gap**)

:::

???

??? Checkpoint

Considerando o checkpoint acima e sabendo que o *Shell Sort* é um algoritmo pensado para ser uma **melhoria** do *Insertion Sort* nas situações em que o mesmo **não performaria bem**, realizando ordenações em gaps e por fim um próprio *Insertion Sort* (quando gap = 1), reflita: 

Qual seria a **complexidade do pior caso** do *Shell Sort*? Será que dependendo do caso, o pior caso do *Shell Sort* pode ser pior do que o pior caso do *Insertion Sort*?

::: Gabarito

A **complexidade** do algoritmo *Shell Sort* continua sendo quadrática pois inclui o *Insertion Sort* no final, mas não fica pior do que isso, pois a somatória de tudo que vem antes do gap = 1 (*Insertion Sort*) não tem como ser pior do que quadrático. Na pratica, espera-se que o *Insertion Sort* final seja mais rápido pois o vetor ja esta mais ordenado que antes.

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

**Observação final**:
- A estratégia utilizada neste handout da sequência de **gaps** ser sempre **dividida por 2** até chegarmos no *Insertion Sort* não é necessáriamente a melhor. O *Shell Sort* é um **framework** e existem **diversas estratégias de sequências de gaps**, que inclusive, podem garantir um tempo melhor do que quadrático.

Caso tenha curiosidade, algumas das outras estratégias conhecidas são:

- **Knuth's increments**
- **Sedgewick's increments**
- **Hibbard's increments**
- **Papernov & Stasevich increment**
- **Pratt**