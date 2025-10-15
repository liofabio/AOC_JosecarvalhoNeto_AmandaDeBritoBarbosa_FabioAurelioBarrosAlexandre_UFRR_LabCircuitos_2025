# Contador Síncrono de 3 e 4 Bits

Este relatório detalha a implementação e o funcionamento de contadores síncronos de 3 e 4 bits. O projeto utiliza o Flip-Flop Tipo T como bloco de memória fundamental. A análise cobre a unidade básica (Flip-Flop T) e a arquitetura dos dois contadores.

---

## 1. Bloco Fundamental: Flip-Flop Tipo T (Toggle)

O Flip-Flop Tipo T é o componente central deste projeto. Ele é um circuito de memória sequencial que tem a capacidade de "bascular" (inverter seu estado) a cada pulso de clock, dependendo do valor de sua entrada `T`.

#### Definição Lógica

A principal função do Flip-Flop T é manter o estado anterior quando a entrada `T` é `0` e inverter o estado da saída `Q` quando a entrada `T` é `1`. A transição ocorre na borda de subida ou descida do clock.

**Tabela Verdade:**

| T | Q (estado atual) | Q (próximo estado) | Descrição           |
|:-:|:----------------:|:------------------:|:--------------------|
| 0 |        0         |         0          | Manter (Hold)       |
| 0 |        1         |         1          | Manter (Hold)       |
| 1 |        0         |         1          | Bascular (Toggle)   |
| 1 |        1         |         0          | Bascular (Toggle)   |

#### Circuito Simulado 

<img width="603" height="408" alt="Image" src="https://github.com/user-attachments/assets/296cc23d-3a1a-479c-a896-893f6fcb07de" />

* **Componentes Utilizados:**
    * 6 Portas **NAND**
    * 3 Inversores (**NOT**)

* **Função Lógica:**
  O circuito é essencialmente um Flip-Flop JK com as entradas J e K conectadas juntas, formando a entrada única `T`. Ele também possui entradas assíncronas `SET` e `RESET` para forçar a saída para um estado específico, independentemente do clock.
  * Quando `T=0`, o flip-flop mantém o estado atual.
  * Quando `T=1`, o flip-flop inverte o estado atual a cada pulso de clock.

---

## 2. Contador Síncrono de 3 Bits

Este circuito é capaz de contar de 0 (000) a 7 (111) de forma síncrona, o que significa que todos os flip-flops compartilham o mesmo sinal de clock.

#### Definição Lógica

A lógica de um contador síncrono garante que as transições de estado de todos os flip-flops ocorram simultaneamente. A entrada `T` de cada flip-flop é controlada pelas saídas dos flip-flops anteriores para determinar quando ele deve bascular.

* `FF0` (LSB): Bascula a cada pulso de clock (`T0 = 1`).
* `FF1`: Bascula quando `Q0` for `1` (`T1 = Q0`).
* `FF2` (MSB): Bascula quando `Q0` e `Q1` forem `1` (`T2 = Q0 AND Q1`).

#### Circuito Simulado 

<img width="636" height="387" alt="Image" src="https://github.com/user-attachments/assets/a000bd41-0a5e-4511-877f-bac54a61f4d2" />

* **Componentes Utilizados:**
    * 3 módulos **Flip-Flop Tipo T**
    * 1 Porta **AND**

* **Funcionamento:**
    1.  O sinal de `CLOCK` é conectado a todos os flip-flops.
    2.  A entrada `T` do primeiro flip-flop (`FF0`) é mantida em nível lógico alto (`1`), fazendo-o bascular a cada pulso.
    3.  A entrada `T` de `FF1` é conectada à saída `Q0` de `FF0`.
    4.  A entrada `T` de `FF2` é conectada à saída de uma porta `AND` que tem `Q0` e `Q1` como entradas.
    5.  As entradas `RESET` permitem que o contador seja zerado a qualquer momento.

---

## 3. Contador Síncrono de 4 Bits

Ampliando o projeto anterior, este circuito conta de 0 (0000) a 15 (1111).

#### Definição Lógica

A lógica de controle para o quarto flip-flop segue o mesmo padrão: ele só deve bascular quando todos os bits anteriores (`Q0`, `Q1` e `Q2`) estiverem em nível lógico `1`.

* `FF0`: `T0 = 1`
* `FF1`: `T1 = Q0`
* `FF2`: `T2 = Q0 AND Q1`
* `FF3`: `T3 = Q0 AND Q1 AND Q2`

#### Circuito Simulado 

<img width="717" height="347" alt="Image" src="https://github.com/user-attachments/assets/6ba2758b-2cd5-4df6-9790-7becb8226634" />

* **Componentes Utilizados:**
    * 4 módulos **Flip-Flop Tipo T**
    * 2 Portas **AND** (uma com 2 entradas e outra com 3, ou duas de 2 entradas em cascata).

* **Funcionamento:**
    A estrutura é idêntica à do contador de 3 bits, com a adição do quarto flip-flop (`FF3`). A entrada `T` deste novo flip-flop é controlada pela saída de uma porta `AND` que verifica se `Q0`, `Q1` e `Q2` são `1`.

#### Análise e Teste de Unidade (para ambos os contadores)

1.  **Reset:** Primeiro, aplica-se um pulso na entrada `RESET` para garantir que todas as saídas (`Q0` a `Qn`) comecem em `0`.
2.  **Contagem:** Aplica-se uma sequência de pulsos na entrada `CLOCK`.
3.  **Verificação:** Após cada pulso, o estado das saídas é verificado para confirmar se corresponde à sequência binária correta.
    * **Contador de 3 bits:** A saída deve seguir a sequência: 000 → 001 → 010 → 011 → 100 → 101 → 110 → 111 → 000...
    * **Contador de 4 bits:** A saída deve seguir a sequência: 0000 → 0001 → ... → 1110 → 1111 → 0000...
4.  **Teste de Set (Opcional):** A entrada `SET` pode ser usada para forçar a saída para o estado máximo (todos os bits em 1), verificando a transição para 0 no próximo pulso de clock.
