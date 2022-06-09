Mattar's Part
======

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

Caso tenha curiosidade, algumas das estratégias conhecidas são:

- **Knuth's increments**
- **Sedgewick's increments**
- **Hibbard's increments**
- **Papernov & Stasevich increment**
- **Pratt**