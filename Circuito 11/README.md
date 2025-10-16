# Extensor de Sinal de 4 bits para 8 bits

## Definição

Um extensor de sinal é um circuito criado para converter um número com sinal *n* bits para um número com sinal de *n* bits, sem que seu **valor e sinal** sejam alterados no processo. Para isso, o circuito utiliza o conceito de complemento de 2, uma forma de representar números negativos em binário.

No esquema proposto, foi usado um barramento de **entrada de 4 bits** direcionado para um barramento de **saída de 8 bits**.

Está organizado da seguinte maneira: A entrada com barramento de 4 bits, onde o fio 3 representa o bit mais significativo, é o bit que determina o sinal do número. A saída com barramento de 8 bits, onde os fios 4, 5, 6 e 7 estão ligados ao bit mais significativo da entrada (3), usados para replicar o valor/sinal, e assim estender o número sem que haja perda de significado. 

<img width="332" height="281" alt="Image" src="https://github.com/user-attachments/assets/1ec4afdc-b371-4219-be67-3152d0da4f40" />

---

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

---

## Exemplo de Funcionamento

O número -5 é representado usando o complemento de dois por 1101. Na conversão, os mesmos bits se mantém, porém os 4 bits adicionais serão a repetição do bit mais esquerda (o MSB), que resultará em 1111 1011.

<img width="309" height="268" alt="Image" src="https://github.com/user-attachments/assets/e15fd5ab-4fe2-408b-ab6b-57807ef4242a" />

