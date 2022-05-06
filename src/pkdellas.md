Parte do Paulo
======

Usando a mesma lógica do *insertion sort*, vamos descartar a ideia de usar os elementos adjacentes do vetor. Ao invés disso, vamos colocar um intervalo entre os elementos a serem comparados. 

A comparação e o deslocamento dos menores elementos para esquerda era da seguinte maneira:

![](insertion_sort.png)

Agora, vamos pensar da seguinte maneira, onde o intervalo é connhecido como **gap**:

![](shellsort_1_gap.png)

A idéia aqui é você comparar o elemento atual com um outro "mais longe", a um gap de distância. Se o próximo elemento for menor que o primeiro, troca, senão, faça nada.


Beleza, mas o que isso vai nos ajudar? Inicialmente, parece até um pouco estranho fazer isso, mas essa lógica é a chave para combater uma das fraquezas do *insertion sort*: quanto mais pra direita estiver um número pequeno, mais deslocamentos ele precisa fazer para a esquerda. 

Um pouco confuso? Tudo bem, vamos explorar essa idéia um pouco mais pra frente, por isso, vamos focar primeiro no funcionamento do algoritimo.

??? Checkpoint 1

Note que ao andarmos ao longo do vetor com um gap específico, é como se estivéssemos separando-o em subvetores, ou conjuntos. Vamos tentar visualizar isso. A partir do vetor abaixo, escreva esses conjuntos a serem comparados com um gap de 2. 

![](vetor_1.png)

::: Gabarito
![](gabarito_check_1.png)

Note que {red}(não) foi realizado as trocas dos elementos, só fizemos a separação dos conjuntos.
:::

???

A partir desses subconjuntos, vamos aplicar a lógica do *insertion do sort*. 

??? Checkpoint 2
Aplique o conceito do *insertion sort* em todos os subvetores obtidos no checkpoint 1. Nesse caso, escreva como ficará o vetor no final de cada troca ao longo dos elementos.

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

Assim, ficamos com o vetor ordenado da maneira abaixo. Simples, certo? E é assim que o *shell sort* funciona. O legal desse algoritimo é a sua similaridade com o *insertion sort*!

![](vetor_2.png)

Vamos discutir um pouco agora. A essa altura do campeonato, pode ser que você teve alguns desses questionamento ao longo do handout:

1. Como eu decido meu gap? 

2. O gap é sempre o mesmo para todas iterações? Isso não fará com que eu pule alguns elementos para sempre?

E se você não pensou nisso, refaça este handout de novo. PERA, to zuando. Enfim, para aqueles que não se perguntaram isso, vamos explicar algumas regras do *shell sort*.

O gap inicialmente começa com um valor referente ao vetor. No nosso caso, adotamos o gap inical como a metade do tamanho do vetor, ou seja, 

$$ gap = \frac{n}{2}$$

Logo, seguindo a lógica dessa sequência, o gap ficará assim:


$$ gap = \frac{n}{2}, \frac{n}{4}, \frac{n}{8}, . . . $$

e isso continua até o *gap ser igual a 1*.

Ué, mas a gente não adotou o gap incialmente a 2? E o tamanho do vetor é 8...algo de errado não está certo!

Pera lá, a verdade é que fizemos isso pra facilitar o entendimento do algoritimo. E se você estiver pensando o mesmo do que eu...sim, o vetor está errado lá em cima...

Então vamos fazer o *shell sort* de verdade, agora seguindo as regras descritas acima.

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

Antes de partir para a última etapa quando gap é igual a 1, por acaso não fica uma pulga atrás da orelha quando a gente faz um *shell sort* de intervalo 1? Pense bem, se estamos comparando o elemento atual com o próximo a uma distância igual a 1, basicamente estamos comparando o elemento adjacente! Isso soa familiar? Sim, é a mesma coisa do que fazer um *insertion sort*!

Com isso em mente, vamos realizar a última etapa da ordenação deste vetor!

??? Checkpoint 5
Realize a última etapa de ordenação do vetor, com um gap = 1, ou seja, um *insertion sort*!

::: Gabarito
![](gabarito_check_5.png)

:::

???