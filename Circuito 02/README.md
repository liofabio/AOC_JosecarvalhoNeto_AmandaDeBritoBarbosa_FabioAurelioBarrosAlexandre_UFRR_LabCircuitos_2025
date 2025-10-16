# Multiplexador de 4 bits

## Definição

Um multiplexador é um circuito lógico que funciona permitindo que apenas uma de suas entradas seja enviada para a saída. Essa seleção é determinada por chaves seletoras, que conduzem os sinais para a saída esperada.

No exemplo implementado, o multiplex apresenta 4 entradas (4 bits), 2 chaves (2 bits) e 1 saída (1 bit). Uma das entradas D0, D1, D2 e D3 será enviada para a saída de acordo com as combinações das chaves seletoras.

## Circuito Lógico

<img width="555" height="489" alt="Image" src="https://github.com/user-attachments/assets/53ca3271-4ca6-4de8-b7dc-79ad432b5e90" />

## Tabela Verdade

Podemos ver as possibilidades na seguinte tabela.

| S0 (Chave 1) | S1 (Chave 2) | Saída |
|:------------:|:------------:|:-----:|
|       0      |       0      |   D0  |
|       0      |       1      |   D1  |
|       1      |       0      |   D2  |
|       1      |       1      |   D3  |


## Exemplo de Funcionamento

Para exemplificar, o teste será para a saída D0. Para isso, S1 é 0, passando pelo inversor, se torna 1. S2 é 0, passando pelo inversor se torna 1. A primeira porta AND recebe 1 do D0, portanto passa a receber os valores 1 1 1.

Considerando a lógica da tabela verdade, uma porta AND tem saída como verdadeira quando todos os seus valores são verdadeiros, e falsa quando pelo menos um dos valores é falso. Nesse caso, a saída será verdadeira, pois todos os valores recebidos são verdadeiros, enquanto nas outras portas pelo menos 1 entrada foi 0 (falsa).

A porta OR no fim do circuito, reúne as saídas das portas AND e tem saída verdadeira quando pelo menos 1 entrada for verdadeira. O mesmo acontece nas entradas D1, D2 e D3, com as respectivas combinações da chave.

<img width="559" height="442" alt="Image" src="https://github.com/user-attachments/assets/40d91629-87cf-45f4-9209-980b78f88891" />
