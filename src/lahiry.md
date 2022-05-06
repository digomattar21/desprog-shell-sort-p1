Shell Sort 🐚
======

Concha o que?
---------

![shell](shell.jpg)

Como o nome já sugere, o **Shell Sort** é um algoritmo computacional de **ordenação**, ou seja, ele serve para solucionar o problema de ordenação de alguma lista de elementos que **não** estão em ordem. Como vimos em aula, cada algoritmo de ordenação tem suas **vantagens e desvantagens**. Nesse handout iremos entender em quais situações o *Shell Sort* é um algoritmo interessante de ser utilizado e como que ele funciona.

Relembrando o conceito de ordenação
---------

Antes de começar a falarmos sobre algoritmos de ordenação, vamos pensar intuitivamente em **como checar se uma lista de elementos já esta em ordem**:

??? Checkpoint

Considere os elementos vizinhos de uma lista `md v`:

* `md v[0]`;

* `md v[1]`;

* `md v[2]`;

e assim consecutivamente. Se a lista `md v` **já está ordenada** (e por ordenada, quero dizer ordem crescente), o que podemos afirmar em relação a todos esses elementos?

::: Gabarito
Podemos afirmar que, se de fato **a lista está em ordem**, então `md v[0]` é certamente menor ou igual que `md v[1]`, que é menor ou igual que `md v[2]` e assim em diante.
:::

???

Tendo em vista o conceito apresentado acima, basta que **apenas um** par de elementos vizinhos viole a condição do elemento `md v[i - 1]` ser maior que o elemento `md v[i]`, para que a lista esteja **desordenada** (caos ಥ_ಥ ). 

Insertion Sort
---------
  
Ainda antes de começar a introdução do algoritmo *Shell Sort* propriamente dito, vamos fazer uma breve revisão do *Insertion Sort*. *Insertion Sort*? Não entendi. Calma aí jovem, tudo vai se esclarecer em seu devido momento.

??? Revisão

Veja abaixo o código da implementação do *Insertion Sort*:

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

Traduzindo do C para o português:

```md
para todo i de 1 a n-1
    temp = v[i]
    encontre um índice j entre 0 e i-1 para "inserir" temp, sem estragar a ordenação
    desloque todos os elementos entre j e i-1 para a direita, sobrescrevendo v[i]
    v[j] = temp
```

Utilize a animação abaixo para simular o funcionamento do *Insertion Sort*:

:insertion

???

??? Checkpoint

Tendo revisado o funcionamento do *Insertion Sort*, considere a lista abaixo:

``` c
int v[] = {4, 8, 6, 7, 5}
```

Simule o algoritmo de ordenação *Insertion Sort* escrevendo o estado da lista no **FINAL** de cada iteração do loop **EXTERNO**.

::: Gabarito
```
4 8 6 7 5
4 6 8 7 5
4 6 7 8 5
4 5 6 7 8
```
:::

???



Shell Sort
---------

Finalmente meus colegas programadores! Vamos começar a aprender o *Shell Sort* propriamente dito. Mas espera aí... Na verdade já temos uma boa noção de como esse algoritmo funciona! Isso porque o *Shell Sort* nada mais é do que uma **melhoria do algortimo de ordenação *Insertion Sort***. 

??? Checkpoint

Vamos lá, pensem em qual é a situação na qual o *Insertion Sort* terá um número elevado de iterações, possuindo alta complexidade.

::: Gabarito
Quando temos uma lista cujos **elementos menores estão muito à direita**, precisaremos de **mais iterações** para conseguir ordenar essa lista com o *Insertion Sort*
:::

???

Ok, entedemos qual é a situação na qual o *Insertion Sort* não performa tão bem, mas e se ao invés de pegarmos o elemento **adjacente**, como seria se o **intervalo entre os números fosse maior?**