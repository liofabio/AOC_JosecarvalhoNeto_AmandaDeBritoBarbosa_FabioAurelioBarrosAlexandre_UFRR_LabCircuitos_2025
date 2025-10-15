# Extensor de Sinal de 4 bits para 8 bits

## Definição

Um extensor de sinal é um circuito criado para converter um número com sinal n bits para um número com sinal de n bits, sem que seu valor e sinal sejam alterados no processo.

No esquema proposto, foi usado um barramento de entrada de 4 bits direcionado para um barramento de saída de 8 bits.

## Tabela Verdade

Podemos ver as possibilidades de combinação para expansão (2^4 = 16) na seguinte tabela.

| Número Decimal |    Entrada   |     Saída    |
|:--------------:|:------------:|:------------:|
|        0       |     0000     |   0000 0000  |
|        1       |     0001     |   0000 0001  |
|        2       |     0010     |   0000 0010  |
|        3       |     0011     |   0000 0011  |
|        4       |     0100     |   0000 0100  |
|        5       |     0101     |   0000 0101  |
|        6       |     0110     |   0000 0110  |
|        7       |     0111     |   0000 0111  |
|       -8       |     1000     |   1111 1000  |
|       -7       |     1001     |   1111 1001  |
|       -6       |     1010     |   1111 1010  |
|       -5       |     1011     |   1111 1011  |
|       -4       |     1100     |   1111 1100  |
|       -3       |     1101     |   1111 1101  |
|       -2       |     1110     |   1111 1110  |
|       -1       |     1111     |   1111 1111  |

## Circuito Lógico

![Diagrama do Multiplexador de 4 entradas](image_2d491c.png)


## Exemplo de Funcionamento

Para exemplificar, o teste será para a saída D0. Para isso, S1 é 0, passando pelo inversor, se torna 1. S2 é 0, passando pelo inversor se torna 1. A primeira porta AND recebe 1 do D0, portanto passa a receber os valores 1 1 1.

Considerando a lógica da tabela verdade, uma porta AND tem saída como verdadeira quando todos os seus valores são verdadeiros, e falsa quando pelo menos um dos valores é falso. Nesse caso, a saída será verdadeira, pois todos os valores recebidos são verdadeiros, enquanto nas outras portas pelo menos 1 entrada foi 0 (falsa).

A porta OR no fim do circuito, reúne as saídas das portas AND e tem saída verdadeira quando pelo menos 1 entrada for verdadeira. O mesmo acontece nas entradas D1, D2 e D3, com as respectivas combinações da chave.
