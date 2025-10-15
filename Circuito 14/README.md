# Detector de Paridade Ímpar

## Definição

O detector de paridade ímpar é um circuito projetado para verificar se o número de bits com valor 1 em um conjunto de entrada é par ou ímpar.

Para elaboração do circuito , foi considerado 4 bits de entrada, havendo a possibilidade de verificação dos números de 0 à 15 (2^4 = 16).  

O circuito está organizado com portas AND e OR, com 3 entradas A, B e D. Na parte superior, duas entradas A e B estão conectadas a portas AND, na qual o resultado é reunido por uma porta OR.  

O resultado desse primeiro bloco, se torna a entrada “A” da parte inferior, que se configura da mesma maneira e resulta em uma saída S final.  

Esse circuito nada mais é do que a representação em módulos da porta XOR, que apresenta o mesmo comportamento, de forma mais simplificada.

## Tabela Verdade

Podemos ver as possibilidades de combinação para expansão (2^4 = 16) na seguinte tabela.

| Número Decimal |    Entrada   |  Nº de Bits  |   Saída   | 
|:--------------:|:------------:|:------------:|:----------|
|        0       |     0000     |    0 (par)   |     0     | 
|        1       |     0001     |   1 (ímpar)  |     1     |
|        2       |     0010     |   1 (ímpar)  |     1     |
|        3       |     0011     |    2 (par)   |     0     |
|        4       |     0100     |   1 (ímpar)  |     1     |
|        5       |     0101     |    2 (par)   |     0     |
|        6       |     0110     |    2 (par)   |     0     |
|        7       |     0111     |   3 (ímpar)  |     1     |
|        8       |     1000     |   1 (ímpar)  |     1     |
|        9       |     1001     |    2 (par)   |     0     |
|       10       |     1010     |    2 (par)   |     0     |
|       11       |     1011     |   3 (ímpar)  |     1     |
|       12       |     1100     |    2 (par)   |     0     |
|       13       |     1101     |   3 (ímpar)  |     1     |
|       14       |     1110     |   3 (ímpar)  |     1     |
|       15       |     1111     |   4 (ímpar)  |     0     |

## Circuito Lógico

![Diagrama do Multiplexador de 4 entradas](image_2d491c.png)


## Exemplo de Funcionamento

O número 12 possui 2 números “1” na sua representação em binário (1100). A quantidade (2) é par, logo a saída será 0.  

O número 7 possui 3 números “1” em binário (0111), logo a quantidade de números “1” é ímpar, então a saída do circuito será 1.
