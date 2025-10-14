# Somador de 8 Bits (A + 4)

Este relatório descreve a concepção e o funcionamento de um circuito somador de 8 bits projetado para executar uma operação específica: adicionar a constante `4` a um número de entrada `A` de 8 bits. A análise abrange desde o bloco de construção fundamental, o Somador Completo de 1 bit, até a arquitetura final de 8 bits.

---

## 1. Bloco Fundamental: Somador Completo de 1 Bit

O componente essencial para a construção do somador é o **Full Adder**, um circuito combinacional que realiza a soma de três bits.

#### Definição Lógica

A função do Full Adder é somar dois bits de entrada (`A` e `B`) mais um bit de "vai-um" (`Carry In` ou `CIN`) vindo de uma etapa anterior. Ele produz como resultado um bit de Soma (`S`) e um bit de "vai-um" para a próxima etapa (`Carry Out` ou `COUT`).

**Tabela Verdade:**

| A | B | CIN | S | COUT |
|:-:|:-:|:---:|:-:|:----:|
| 0 | 0 |  0  | 0 |  0   |
| 0 | 0 |  1  | 1 |  0   |
| 0 | 1 |  0  | 1 |  0   |
| 0 | 1 |  1  | 0 |  1   |
| 1 | 0 |  0  | 1 |  0   |
| 1 | 0 |  1  | 0 |  1   |
| 1 | 1 |  0  | 0 |  1   |
| 1 | 1 |  1  | 1 |  1   |

#### Circuito Simulado (somador-1-bit)

<img width="520" height="343" alt="Image" src="https://github.com/user-attachments/assets/51058078-2fd5-4196-983b-57594a6cc427" />

* **Componentes Utilizados:**
    * 2 Portas **XOR** (OU Exclusivo)
    * 2 Portas **AND** (E)
    * 1 Porta **OR** (OU)

* **Funções Lógicas:**
  * A saída de **Soma (`S`)** é o resultado do OU Exclusivo entre as três entradas:
    ```
    S = A ⊕ B ⊕ CIN
    ```
  * A saída de **"Vai-um" (`COUT`)** é `1` se duas ou mais entradas forem `1`:
    ```
    COUT = (A ∧ B) ∨ (CIN ∧ (A ⊕ B))
    ```


---

## 2. Circuito Principal: Somador de 8 Bits (Ripple-Carry Adder)

Para somar números de 8 bits, oito módulos Full Adder de 1 bit são conectados em cascata.

#### Definição Lógica

O circuito foi projetado para realizar a operação aritmética `Y = A + 4`, onde:
* `A` é uma entrada de 8 bits `[A7, A6, A5, A4, A3, A2, A1, A0]`.
* O número `4` é uma constante, representada em binário de 8 bits como `00000100`.

A soma é realizada bit a bit, da direita para a esquerda (do menos significativo para o mais significativo), propagando o bit de "vai-um" de cada estágio para o próximo.

#### Circuito Simulado (somador-completo)

<img width="358" height="514" alt="Image" src="https://github.com/user-attachments/assets/f72e7dc9-cbc0-4747-93bb-53dc01f53c9e" />

* **Componentes Utilizados:**
    * 8 módulos **Somador Completo de 1 Bit**.

* **Implementação da Função `A + 4`:**
    O circuito implementa a soma fixando o segundo operando (`B`) com o valor binário de 4 (`00000100`). Isso é feito conectando as entradas `b` de cada Full Adder a um nível lógico fixo (0 ou 1):
    * **Entrada `A`**: Conectada aos pinos `A0` a `A7`.
    * **Entrada `B` (constante 4)**:
        * Full Adder 0 (`S0`): entrada `b` conectada em **0** (`B0`)
        * Full Adder 1 (`S1`): entrada `b` conectada em **0** (`B1`)
        * Full Adder 2 (`S2`): entrada `b` conectada em **1** (`B2`)
        * Full Adders 3 a 7 (`S3`-`S7`): entradas `b` conectadas em **0** (`B3`-`B7`)
    * **Carry In Inicial (`CIN`)**: A entrada `CIN` do primeiro somador (o menos significativo) é conectada em **0** para garantir que a operação seja uma adição pura.
    * **Saída**: O resultado da soma é fornecido pelas saídas `S0` a `S7`, e o "vai-um" final é `COUT`.

#### Análise e Teste de Unidade

Para verificar o funcionamento do circuito, podemos realizar um teste com um valor de exemplo para a entrada `A`.

**Exemplo de Teste:**
* **Entrada:** Seja `A = 13`. Em binário de 8 bits, `A = 00001101`.
* **Operação Esperada:** `Y = 13 + 4 = 17`.
* **Resultado Binário Esperado:** `17 = 00010001`.

**Execução da Lógica (bit a bit):**
* `A` = `00001101`
* `B` = `00000100`
* `CIN` inicial = `0`

1.  **Bit 0:** `S0 = A0+B0+CIN = 1+0+0 = 1`.  `Cout0 = 0`.
2.  **Bit 1:** `S1 = A1+B1+Cout0 = 0+0+0 = 0`.  `Cout1 = 0`.
3.  **Bit 2:** `S2 = A2+B2+Cout1 = 1+1+0 = 0`.  `Cout2 = 1`.
4.  **Bit 3:** `S3 = A3+B3+Cout2 = 1+0+1 = 0`.  `Cout3 = 1`.
5.  **Bit 4:** `S4 = A4+B4+Cout3 = 0+0+1 = 1`.  `Cout4 = 0`.
6.  **Bit 5:** `S5 = A5+B5+Cout4 = 0+0+0 = 0`.  `Cout5 = 0`.
7.  **Bit 6:** `S6 = A6+B6+Cout5 = 0+0+0 = 0`.  `Cout6 = 0`.
8.  **Bit 7:** `S7 = A7+B7+Cout6 = 0+0+0 = 0`.  `Cout7 (final) = 0`.

**Resultado Obtido:** A saída `S` é `[S7...S0] = 00010001`, que corresponde ao decimal **17**. O `COUT` final é `0`, indicando que não houve estouro (overflow). O teste confirma que o circuito opera corretamente.
