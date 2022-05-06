#
## Implementação do Shell Sort na prática
	

   ```
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

Esse algoritimo é extremamente utilizado quando uma recursão excede o limite ou quando o uso do insertion sort por conta de números próximos estarem muito afastados um do outro seria equivocado, pois o shell sort faria uma menor quantidade de trocas para ordenar o array.

## Complexidade de tempo do Shell Sort
O Shell Sort não possui estabilidade devido ao fato de não “observar” ou melhor, processar dados que estão no meio do gap.

A complexidade de tempo do algoritimo varia de acordo com a sequência de incremento escolhida, sendo a melhor sequência de incremento desconhecida.


| Melhor      | Media        | Pior |       
| :---        |    :----:    |---:  |
|O(n* log n)  | O(n* log n)  |O(n^2)|

Em seu melhor caso, a complexidade do algoritimo fica O(n * log n), esse caso ocorre quando o array já está ordenado o número de comparações para cada incremento é igual ao tamanho do array.





