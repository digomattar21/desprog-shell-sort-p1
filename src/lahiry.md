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