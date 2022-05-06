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

Usando a mesma lógica do *Insertion Sort*, vamos descartar a ideia de usar os elementos adjacentes do vetor. Ao invés disso, vamos colocar um intervalo entre os elementos a serem comparados. 

A comparação e o deslocamento dos menores elementos para esquerda era da seguinte maneira:

![](insertion_sort.png)

Agora, vamos pensar da seguinte maneira, onde o intervalo é connhecido como **gap**:

![](shellsort_1_gap.png)

A ideia aqui é você comparar o elemento atual com um outro "mais longe", a um gap de distância. Se o próximo elemento for menor que o primeiro, troca, senão, faça nada.


Beleza, mas o que isso vai nos ajudar? Inicialmente, parece até um pouco estranho fazer isso, mas essa lógica é a chave para combater uma das fraquezas do *Insertion Sort*: quanto mais pra direita estiver um número pequeno, mais deslocamentos ele precisa fazer para a esquerda. 

Um pouco confuso? Tudo bem, vamos explorar essa ideia um pouco mais pra frente, por isso, vamos focar primeiro no funcionamento do algoritimo.

??? Checkpoint

Note que ao andarmos ao longo do vetor com um gap específico, é como se estivéssemos separando-o em subvetores, ou conjuntos. Vamos tentar visualizar isso. A partir do vetor abaixo, escreva esses conjuntos a serem comparados com um gap de 2. 

![](vetor_1.png)

::: Gabarito
![](gabarito_check_1.png)

Note que {red}(não) foi realizado as trocas dos elementos, só fizemos a separação dos conjuntos.
:::

???

A partir desses subconjuntos, vamos aplicar a lógica do *Insertion do Sort*. 

??? Checkpoint
Aplique o conceito do *Insertion Sort* em todos os subvetores obtidos no checkpoint 1. Nesse caso, escreva como ficará o vetor no final de cada troca ao longo dos elementos.

**obs:** Lembre-se, se o próximo elemento for menor que o primeiro, troca, senão, faça nada.

::: Gabarito
```
{33, 31, 40, 8, 12, 17, 25, 42}
{33, 8, 40, 31, 12, 17, 25, 42}
{33, 8, 12, 31, 40, 17, 25, 42}
{33, 8, 12, 17, 40, 31, 25, 42}
{33, 8, 12, 17, 25, 31, 40, 42}
{33, 8, 12, 17, 25, 31, 40, 42}
```
:::

???

Assim, ficamos com o vetor ordenado da maneira abaixo. Simples, certo? E é assim que o *Shell Sort* funciona. O legal desse algoritimo é a sua similaridade com o *Insertion Sort*!

![](vetor_2.png)

Vamos discutir um pouco agora. A essa altura do campeonato, pode ser que você teve alguns desses questionamento ao longo do handout:

1. Como eu decido meu gap? 

2. O gap é sempre o mesmo para todas iterações? Isso não fará com que eu pule alguns elementos para sempre?

E se você não pensou nisso, refaça este handout de novo. PERA, to zuando. Enfim, para aqueles que não se perguntaram isso, vamos explicar algumas regras do *Shell Sort*.

O gap inicialmente começa com um valor referente ao vetor. No nosso caso, adotamos o gap inical como a metade do tamanho do vetor, ou seja, 

$$ gap = \frac{n}{2}$$

Logo, seguindo a lógica dessa sequência, o gap ficará assim:


$$ gap = \frac{n}{2}, \frac{n}{4}, \frac{n}{8}, . . . $$

e isso continua até o *gap ser igual a 1*.

Ué, mas a gente não adotou o gap incialmente a 2? E o tamanho do vetor é 8...algo de errado não está certo!

Pera lá, a verdade é que fizemos isso pra facilitar o entendimento do algoritimo. E se você estiver pensando o mesmo do que eu...sim, o vetor está errado lá em cima...

Então vamos fazer o *Shell Sort* de verdade, agora seguindo as regras descritas acima.

??? Checkpoint
Realize a ordenação do vetor abaixo, só que agora, com o gap = 4. 

![](vetor_1.png)

::: Gabarito
![](gabarito_check_3.png)

Dessa maneira, o vetor ficará ordenado da seguinte maneira:

![](gabarito_check_3_2.png)

:::

???

??? Checkpoint
Seguindo a sequência adotada do gap, vamos dividí-lo por 2. Realize a ordenação do vetor adquirido no exercício anterior, só que agora, com o gap = 2. 

::: Gabarito
![](gabarito_check_4.png)

Dessa maneira, o vetor ficará ordenado da seguinte maneira:

![](gabarito_check_4_2.png)

:::

???

Antes de partir para a última etapa quando gap é igual a 1, por acaso não fica uma pulga atrás da orelha quando a gente faz um *Shell Sort* de intervalo 1? Pense bem, se estamos comparando o elemento atual com o próximo a uma distância igual a 1, basicamente estamos comparando o elemento adjacente! Isso soa familiar? Sim, é a mesma coisa do que fazer um *Insertion Sort*!

Com isso em mente, vamos realizar a última etapa da ordenação deste vetor!

??? Checkpoint
Realize a última etapa de ordenação do vetor, com um gap = 1, ou seja, um *Insertion Sort*!

::: Gabarito
![](gabarito_check_5.png)

:::

???

Implementação do Shell Sort na prática
---------	

```c
void shellSort(int array[], int n) {
  // Rearrange elements at each n/2, n/4, n/8, ... intervals
  for (int interval = n / 2; interval > 0; interval /= 2) {
    for (int i = interval; i < n; i += 1) {
      int temp = array[i];
      int j;
      for (j = i; j >= interval && array[j - interval] > temp; j -= interval) {
        array[j] = array[j - interval];
      }
      array[j] = temp;
    }
  }
}
```

Esse algoritimo é extremamente utilizado quando uma recursão excede o limite ou quando o uso do *Insertion Sort* por conta de números próximos estarem muito afastados um do outro seria equivocado, pois o *Shell Sort* faria uma menor quantidade de trocas para ordenar o array.

Complexidade de tempo do Shell Sort
---------

O *Shell Sort* **não possui estabilidade** devido ao fato de não “observar” ou melhor, processar dados que estão no meio do gap.

A complexidade de tempo do algoritimo varia de acordo com a **sequência de incremento escolhida**, sendo a melhor sequência de incremento desconhecida.


| Melhor      | Media        | Pior |       
| :---        |    :----:    |---:  |
|O(n* log n)  | O(n* log n)  |O(n^2)|

Em seu melhor caso, a complexidade do algoritimo fica **O(n * log n)**, esse caso ocorre quando o array já está ordenado o número de comparações para cada incremento é igual ao tamanho do array.