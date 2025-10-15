# Detector de Número Primo

## Definição
O circuito lógico a seguir foi construído para ser capaz de identificar se um número binário de 4 bits é um número primo ou não.

Foi considerado a adição de 4 entradas (4 bits), totalizando 16 possibilidades (2^4 = 16)

## Funcionamento Geral

O circuito implementado possui 4 entradas (A, B, C, D) correspondente aos 4 bits, uma saída S, e foi construído com a combinação das portas lógicas NOT, AND e OR.  

A entrada A é o bit mais significativo (MSB), enquanto a entrada D é o bit de menor significância (LSB). A saída somente terá valor lógico alto (será 1), se o número de entrada for primo, e terá valor lógico baixo (será 0) caso contrário. 

## Tabela Verdade

|  ABCD (Número Binário)  |  Número Decimal  |     Saída    |
|:-----------------------:|:----------------:|:------------:|
|           0000          |         0        |   0  |
|           0001          |         1        |   0  |
|           0010          |         2        |   1  |
|           0011          |         3        |   1  |
|           0100          |     4     |   0  |
|           0101          |     5    |   0  |
|           0110          |     6    |   0  |
|           0111          |      7    |   1  |
|           1000          |      8     |   0  |
|           1001          |     9     |   0  |
|           1010          |     10     |   0  |
|           1011          |     11     |   1  |
|           1100          |     12     |   0  |
|           1101          |     13     |   1  |
|           1110          |     14     |   0  |
|           1111          |      15     |   0  |

## Exemplo de Funcionamento
O circuito, por ser de 4 bits, identifica os números primos num intervalo de 0 (0000) à 15 (1111), sendo eles 2, 5, 7, 11 e 13.  

Cada porta AND é projetada para identificar um ou mais desses números, em quando a porta OR é usada para reunir os resultados.

- 1ª porta AND: identifica os números 2 (0010) e 3 (0011)
- 2ª porta AND: 3 (0011) e 11 (1011)
- 3ª porta AND: 5 (0101) e 7 (0111)
- 4ª porta AND: 5 (0101) e 13 (1101)
