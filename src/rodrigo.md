Mattar's Part
======

Complexidade de tempo do Shell Sort
---------

O *Shell Sort* é um algoritimo extremamente utilizado quando uma recursão **excede o limite** ou quando o uso do *Insertion Sort* por conta de **números próximos estarem muito afastados um do outro** seria equivocado, pois o *Shell Sort* faria uma menor quantidade de trocas para conseguir ordenar o array.

??? Checkpoint

A partir do conhecimento obtido durante este e handout, sabendo que o *Shell Sort* é um algoritmo pensado para ser uma **melhoria** do *Insertion Sort* nas situações em que o mesmo **não performaria bem**, realizando ordenações em gaps e por fim um próprio *Insertion Sort* (quando gap = 1), reflita: 

Qual seria a **complexidade do pior caso** do *Shell Sort*? Será que dependendo do caso, o pior caso do *Shell Sort* pode ser pior do que o pior caso do *Insertion Sort*? (fun fact: nesse handout a palavra "pior" foi mencionada X vezes)

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