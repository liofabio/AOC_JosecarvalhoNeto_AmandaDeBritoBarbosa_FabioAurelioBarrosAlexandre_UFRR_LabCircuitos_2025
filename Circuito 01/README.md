# Análise de Circuitos Flip-Flop

Este repositório contém a análise, simulação e teste de circuitos sequenciais fundamentais: o **Flip-Flop Tipo D** (em duas variações) e o **Flip-Flop JK Mestre-Escravo**. O objetivo é descrever detalhadamente o funcionamento, a lógica interna e os procedimentos de verificação de cada circuito.

---

## 1. Flip-Flop Tipo D (Data)

O Flip-Flop Tipo D é um bloco de construção essencial em sistemas digitais para o armazenamento de um bit de informação. Sua principal característica é transferir o valor da entrada `D` (Dados) para a saída `Q` de forma sincronizada com um sinal de controle.

### 1.1. Flip-Flop D com Clock

Esta é a implementação síncrona padrão, sensível à borda do clock.

#### Definição Lógica

A saída `Q` amostra e armazena o valor da entrada `D` no momento da transição ativa do sinal de `CLOCK`. Fora dessa transição, a saída permanece inalterada.

**Tabela Verdade:**

| Clock | D | Q (próximo estado) | Descrição           |
| :---: | :-: | :----------------: | ------------------- |
|   ↑   | 0 |         0          | Armazena 0 (Reset)  |
|   ↑   | 1 |         1          | Armazena 1 (Set)    |
| 0/1/↓ | X | Q (estado anterior) | Mantém o estado     |

*O símbolo `↑` representa a borda de subida do clock. `X` significa "não importa" (don't care).*

#### Circuito Simulado

<img width="606" height="238" alt="Image" src="https://github.com/user-attachments/assets/9786664d-e9a3-46a7-b633-aafefac98a98" />

* **Pinos:**
    - **Entradas:** `D` (Data), `CLOCK`
    - **Saídas:** `Q` (saída principal), `~Q` (saída invertida)

* **Função Lógica:**
  A equação característica que descreve seu comportamento é:
   Q_{próximo} = D 

#### Análise e Teste de Unidade
O teste de verificação segue os passos abaixo:
1.  **Manter Estado:** Com `CLOCK` em nível baixo, alterne o valor de `D`. A saída `Q` não deve sofrer alterações.
2.  **Armazenar 0:** Com `D=0`, aplique um pulso de `CLOCK` (0 → 1 → 0). A saída `Q` deve transicionar para `0`.
3.  **Armazenar 1:** Com `D=1`, aplique um pulso de `CLOCK`. A saída `Q` deve transicionar para `1`.

---

### 1.2. Flip Flop D com ENABLE 

Esta variação utiliza um sinal de habilitação (`ENABLE`) em vez de um clock de borda. O circuito é "transparente" enquanto o sinal de `ENABLE` está ativo.

#### Definição Lógica

A saída `Q` segue o valor da entrada `DATA` continuamente, enquanto `ENABLE` estiver em nível lógico alto (1). Quando `ENABLE` vai para `0`, o último valor de `Q` é "travado" (latched).

**Tabela Verdade:**

| ENABLE | D | Q (próximo estado) | Descrição                |
| :----: | :-: | :----------------: | ------------------------ |
|    1   | 0 |         0          | Modo Transparente (Q=D)  |
|    1   | 1 |         1          | Modo Transparente (Q=D)  |
|    0   | X | Q (estado anterior) | Modo de Memória (Latch)  |

#### Circuito Simulado

<img width="546" height="244" alt="Image" src="https://github.com/user-attachments/assets/46aa2330-9e2f-430f-90ca-c2ba570ab26f" />

* **Pinos:**
    - **Entradas:** `DATA`, `ENABLE`
    - **Saídas:** `Q`, `~Q` (identificadas pelos pontos de saída no circuito)

* **Função Lógica:**
  O circuito implementa um Latch SR controlado pelas entradas. Quando `ENABLE=1`, as entradas `S` e `R` do latch interno são definidas por `DATA` e `~DATA`, respectivamente. Quando `ENABLE=0`, o latch mantém seu estado.

#### Análise e Teste de Unidade
1.  **Modo Memória:** Defina `ENABLE=0`. Altere `DATA`. A saída `Q` deve permanecer inalterada.
2.  **Modo Transparente:** Defina `ENABLE=1`. A saída `Q` deve seguir imediatamente qualquer mudança em `DATA`.
3.  **Teste de Latch:** Com `ENABLE=1` e `DATA=1`, a saída `Q` será `1`. Mude `ENABLE` para `0`. Agora, mude `DATA` para `0`. A saída `Q` deve permanecer em `1`, confirmando o armazenamento.

---

## 2. Flip-Flop JK Mestre-Escravo (Master-Slave)

O Flip-Flop JK é um dos mais versáteis, com modos de operação para manter, setar, resetar e inverter (toggle) a saída. A configuração Mestre-Escravo previne a condição de corrida (*race condition*) ao isolar as entradas das saídas durante a transição do clock.

#### Definição Lógica

As entradas `J` e `K` determinam o próximo estado de `Q` na borda de descida do pulso de clock.

**Tabela Verdade:**

| J | K | Q (próximo estado)  | Descrição              |
| :-: | :-: | :-------------------: | ---------------------- |
| 0 | 0 |  Q (estado anterior)  | Manter (Memória)       |
| 0 | 1 |           0           | Reset (Limpar)         |
| 1 | 0 |           1           | Set (Definir)          |
| 1 | 1 | ~Q (estado anterior) | Toggle (Bascular/Inverter) |

#### Circuito Simulado


<img width="866" height="520" alt="Image" src="https://github.com/user-attachments/assets/aead1a70-99f0-4901-a727-b742cf1810b1" />

* **Pinos:**
    - **Entradas Síncronas:** `J`, `K`, `CLOCK`
    - **Entradas Assíncronas:** `PRESET`, `CLEAR`
    - **Saídas:** `Q`, `~Q`

* **Função Lógica:**  
  A equação característica do Flip-Flop JK é:  **Q(próximo) = (J ∧ ¬Q) ∨ (¬K ∧ Q)**  

  O circuito consiste em dois latches: o **Mestre**, que captura o estado das entradas `J` e `K` quando `CLOCK = 1`, e o **Escravo**, que transfere o estado do Mestre para a saída `Q` quando `CLOCK` transiciona para `0`.


#### Análise e Teste de Unidade
1.  **Teste Assíncrono:**
    * Aplique `PRESET=0` (com `CLEAR=1`). `Q` deve ir para `1` imediatamente, ignorando o clock.
    * Aplique `CLEAR=0` (com `PRESET=1`). `Q` deve ir para `0` imediatamente.
    * Para testes síncronos, `PRESET` e `CLEAR` devem estar em `1`.

2.  **Teste Síncrono (a cada pulso de clock):**
    * **Manter:** `J=0`, `K=0`. A saída `Q` não deve mudar após o pulso.
    * **Reset:** `J=0`, `K=1`. A saída `Q` deve ir para `0` na borda de descida do clock.
    * **Set:** `J=1`, `K=0`. A saída `Q` deve ir para `1` na borda de descida do clock.
    * **Toggle:** `J=1`, `K=1`. A cada pulso de clock, a saída `Q` deve inverter seu estado anterior.
