# Somador de 8 bits

## Definição
O somador é um dos circuitos mais fundamentais para realizar operações aritméticas em computadores. São construídos a partir de circuitos lógicos básicos e são escalonados para manipular números binários de tamanhos variados.  

Ele funciona somando bits individuais e apresentando uma saída com o resultado dessa soma. Algumas somas precisam de mais bits para soma, então uma terceira entrada é adicionada, conhecida como *carry in* ou “vai-um”.

O circuito proposto foi projetado a partir da combinação de somadores de 1 bit.

## Circuito Lógico
<img width="584" height="332" alt="Image" src="https://github.com/user-attachments/assets/df9be50f-ccf3-4db7-8f25-8ab939d3af23" />

---

## Funcionamento

### Somador de 1 bit

O somador de 1 bit soma um número de 1 bit com outro, também de 1 bit. Considerando a maneira como a soma manual é realizada, **a0** seria o primeiro elemento, enquanto **a1**, o segundo elemento. **S** indica o resultado da soma. Um teste será executado para exemplificar.  

A soma entre os números binários 1 + 1 resulta em 10 (em decimal 2). O bit “0” é setado na saída, enquanto o bit “1” é levado para a casa esquerda (conhecido como “vai-um / *carry in*”), para realizar uma nova soma com os elementos da próxima etapa, se houver. 

Se logo no início da operação, o *carry in* for setado (ou se houver um bit de outra operação), o resultado será 1 na saída e 1 no carry out, ou seja 11 (3 em decimal), onde o bit “1” vira o *carry-out*, e será transportado para a próxima etapa da soma.

<img width="456" height="442" alt="Image" src="https://github.com/user-attachments/assets/401cf673-11a1-464a-a092-2cb55183a664" />

---

### Somador de 4 bits

O somador de 4 bits consiste na composição de **4 circuitos de somadores de 1 bit**, onde serão somados um número de 4 bits com outro de 4 bits.  

Nesse contexto, o *carry-out* de um circuito, se torna o *carry-in* do outro, seguindo a mesma lógica da operação realizada manualmente com número decimais, onde é somado aos elementos da coluna à esquerda, e “desce” para compor o resultado.  

O último *carry-out* do 4º circuito, indica se a soma excede a capacidade de representação, sinalizando um **overflow**.

<img width="403" height="282" alt="Image" src="https://github.com/user-attachments/assets/6563a50f-83c4-4677-ba3d-cdb8c33c5fb5" />

---

### Somador de 8 bits

Seguindo a mesma lógica de módulo, o somador de 8 bits consiste na composição de 2 circuitos de 4 bits, somando dois números, ambos de 8 bits.  

De forma similar ao somador de 4 bits, o carry out do primeiro somador, se torna o carry in do segundo somador. O carry out final do segundo somador sinaliza um overflow da soma de 8 bits.

<img width="584" height="332" alt="Image" src="https://github.com/user-attachments/assets/df9be50f-ccf3-4db7-8f25-8ab939d3af23" />

---

## Exemplo de execução
Como exemplo desse circuito, será realizado o teste de soma com os números 172 (10101100) + 40 (00101000), com resultado esperado de 212 (11010100).  

Os **4 bits mais à direita (LSB)** do primeiro somador (bits 0-3), serão somados, e nesse gerarão um *carry out*, pois 1 + 1 = 10, que será encaminhado para o segundo somador (bits 4-7). O bit “0” permanecerá na saída, e o bit “1” que veio da operação anterior como *carry out*, se torna o *carry in* da próxima etapa da soma.   

Esse processo é repetido durante o circuito sempre que necessário, até que encontre o último *carry out*, completando os 8 bits. O *carry out* final do segundo somar resultando em 0 indica que não houve ***overflow**.

<img width="573" height="320" alt="Image" src="https://github.com/user-attachments/assets/2812a4ee-5f3f-4c3c-a6a6-52cd0719f9a7" />

