# Unidade Lógica e Aritmética (ULA) Multifuncional de 8 Bits

Este relatório documenta o projeto e a implementação de uma Unidade Lógica e Aritmética (ULA) de 8 bits. Este circuito complexo representa o núcleo computacional de um processador, sendo capaz de executar um conjunto diversificado de 10 operações, incluindo cálculos aritméticos (soma, subtração), operações lógicas bit a bit (AND, OR, XOR, etc.) e operações de deslocamento (shift left/right). A função a ser executada é selecionada por um código de controle de 4 bits.

---

## 1. Subcircuitos Fundamentais

A ULA é uma arquitetura modular construída a partir de blocos funcionais especializados. Cada bloco realiza uma operação específica em paralelo, e um seletor final escolhe o resultado desejado.

### 1.1. Unidade Aritmética

* **Somador de 8 Bits:** Realiza a adição binária de duas entradas de 8 bits (`A + B`). É a base para a maioria das operações aritméticas.
* **Subtrator de 8 Bits:** Realiza a subtração (`A - B`). Esta operação é implementada de forma eficiente utilizando o somador, através da técnica do **complemento de dois**. A lógica executada é: `A + (NOT B) + 1`.

### 1.2. Unidade de Deslocamento (Shifters)

Os shifters manipulam os dados movendo os bits para a esquerda ou para a direita.

* **Shift-Left (Deslocamento à Esquerda):** Este circuito move cada bit da entrada uma posição para a esquerda. O bit mais à esquerda (MSB) é descartado, e um `0` é inserido na posição mais à direita (LSB). Um deslocamento de `n` bits para a esquerda é equivalente a multiplicar o número por $2^n$. O circuito que implementa o deslocamento de 2 bits realiza uma multiplicação por 4.

<img width="707" height="590" alt="Image" src="https://github.com/user-attachments/assets/de31f857-a873-4fcb-afb1-7bb8e95a2057" />

* **Shift-Right (Deslocamento à Direita):** De forma análoga, este circuito move cada bit uma posição para a direita. O LSB é descartado e um `0` é inserido na posição do MSB (deslocamento lógico). Um deslocamento de `n` bits para a direita é equivalente a uma divisão inteira por $2^n$.

<img width="679" height="509" alt="Image" src="https://github.com/user-attachments/assets/15917e19-1df4-4a2b-bb5d-8489c1babe09" />

### 1.3. Unidade Lógica

Este bloco executa operações lógicas bit a bit, onde cada par de bits correspondente de `A` e `B` é processado de forma independente. As funções implementadas são: **AND, OR, NOT, NOR, NAND, XOR**.

### 1.4. Multiplexador de Seleção 16x1 (8 bits)

Este é o componente de controle que torna a ULA programável. Embora o projeto utilize 10 operações, um MUX 16x1 (com 4 bits de seleção) é usado para selecionar qual dos 10 resultados calculados em paralelo será enviado para a saída final.

<img width="513" height="337" alt="Image" src="https://github.com/user-attachments/assets/30a5072f-41ed-4f59-ac80-562ff893f44f" />

---

## 2. A ULA de 8 Bits (Circuito Principal)

O circuito principal integra todos os subcomponentes, direcionando as entradas para todas as unidades e usando o multiplexador para selecionar a saída final.

#### Definição Lógica

A ULA recebe duas entradas de 8 bits (`A` e `B`) e um código seletor (`SELETOR`) de 4 bits. Ela produz uma única saída de 8 bits que corresponde ao resultado da operação escolhida pelo seletor.

#### Tabela de Operações

O código de 4 bits `SELETOR` determina a função da ULA conforme a tabela abaixo:

| SELETOR (Binário) | Operação Realizada          |
|:-----------------:|:----------------------------|
|       `0000`      | `A AND B`                   |
|       `0001`      | `A OR B`                    |
|       `0010`      | `NOT A`                     |
|       `0011`      | `A NOR B`                   |
|       `0100`      | `A NAND B`                  |
|       `0101`      | `A XOR B`                   |
|       `0110`      | `SHIFT 2 BITS ESQUERDA (A)` |
|       `0111`      | `SHIFT 2 BITS DIREITA (A)`  |
|       `1000`      | `SOMADOR (A + B)`           |
|       `1001`      | `SUBTRADOR (A - B)`         |

#### Circuito Simulado

<img width="628" height="538" alt="Image" src="https://github.com/user-attachments/assets/7c6e4a49-5f2e-4397-a8d7-46cbd55fedae" />

* **Funcionamento:**
    1.  Os operandos `A` e `B` são distribuídos para as entradas de todos os 10 blocos funcionais.
    2.  Todos os blocos (Somador, Subtrator, AND, etc.) calculam seus resultados em paralelo.
    3.  O `SELETOR` de 4 bits é fornecido às entradas de controle do multiplexador principal.
    4.  O multiplexador seleciona, dentre os 10 barramentos de resultados, aquele que corresponde ao código do seletor e o encaminha para a `SAÍDA`.

#### Análise e Teste de Unidade

O teste da ULA é feito validando cada uma das suas 10 funções.

1.  **Teste Aritmético (Subtração):**
    * **Objetivo:** Calcular `50 - 25 = 25`.
    * **Passos:**
        1.  Definir `A = 00110010` (50).
        2.  Definir `B = 00011001` (25).
        3.  Definir `SELETOR = 1001`.
        4.  **Verificar:** A `SAÍDA` deve ser `00011001` (25).

2.  **Teste Lógico (NAND):**
    * **Objetivo:** Calcular `11110000 NAND 10101010`.
    * **Passos:**
        1.  Definir `A = 11110000`.
        2.  Definir `B = 10101010`.
        3.  Definir `SELETOR = 0100`.
        4.  **Verificar:** A `SAÍDA` deve ser `01011111`.

3.  **Teste de Deslocamento (Shift Left 2 bits):**
    * **Objetivo:** Multiplicar `15` por `4` (resultado `60`).
    * **Passos:**
        1.  Definir `A = 00001111` (15).
        2.  Definir `SELETOR = 0110`.
        3.  **Verificar:** A `SAÍDA` deve ser `00111100` (60).

Ao verificar cada código de operação com entradas de teste adequadas, a funcionalidade completa da ULA é validada, concluindo com sucesso a construção do componente computacional mais crucial de um processador.
