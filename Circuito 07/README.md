# Banco de Registradores 

Este relatório descreve a arquitetura e o funcionamento de um Banco de Registradores, um componente fundamental na arquitetura de computadores. Este circuito funciona como uma memória pequena e ultrarrápida, capaz de armazenar múltiplos dados (palavras de 8 bits) e de acessá-los individualmente para operações de leitura e escrita. O projeto é modular, construído a partir de subcircuitos como Flip-Flops, Registradores, Multiplexadores e Demultiplexadores.

---

## 1. Subcircuitos Fundamentais

A construção do banco de registradores depende de vários blocos de construção lógicos.

### 1.1. Flip-Flop Tipo T (Toggle)

O elemento de memória mais básico utilizado é o Flip-Flop T. Sua função é armazenar um único bit e bascular (inverter seu estado) quando a entrada `T` está em nível alto e um pulso de clock é recebido. Ele é a base para a criação dos registradores.

<img width="502" height="296" alt="Image" src="https://github.com/user-attachments/assets/73e10bc4-6140-455a-aa19-4523e7d55a0a" />

### 1.2. Registrador de 8 Bits

Para armazenar uma palavra de 8 bits, oito flip-flops são agrupados para formar um **Registrador de 8 Bits**. Este subcircuito possui 8 entradas de dados paralelas e 8 saídas paralelas. Quando o sinal de carga (`load`) está ativo, no momento do pulso de clock, os 8 bits da entrada são armazenados simultaneamente nos flip-flops.

<img width="764" height="371" alt="Image" src="https://github.com/user-attachments/assets/2a7e2a67-51c4-44dd-93ce-7e4b41386302" />

### 1.3. Multiplexadores (MUX)

Os multiplexadores são essenciais para a **operação de leitura**. Eles funcionam como chaves seletoras, escolhendo qual dos registradores terá seu dado enviado para a saída. O projeto utiliza uma hierarquia de multiplexadores para chegar ao seletor final:

* **Mult 2x1:** Seleciona uma de duas entradas de 1 bit.
* **Mult 2x1 (8 bits):** Usa oito MUXes 2x1 para selecionar um de dois barramentos de 8 bits.
* **Mult 4x1 (8 bits):** Combina MUXes 2x1 (8 bits) para selecionar um de quatro barramentos de 8 bits.
* **Mult 8x1 (8 bits):** O componente final, usado na saída do banco. Ele recebe os dados de 8 registradores diferentes e, com base em uma chave de seleção de 3 bits, direciona um deles para a saída.

<img width="651" height="305" alt="Image" src="https://github.com/user-attachments/assets/8669face-9fbb-4b1a-9d3f-0df414308f87" />

### 1.4. Demultiplexador 1-para-8 (DEMUX)

O demultiplexador é crucial para a **operação de escrita**. Ele faz o oposto do MUX: pega uma única linha de entrada e a direciona para uma das oito linhas de saída, conforme determinado por uma chave de seleção de 3 bits. No nosso circuito, a entrada do DEMUX é o sinal de `LOAD` (habilitado pelo clock), e as saídas habilitam a escrita em apenas **um** dos oito registradores por vez.

<img width="594" height="571" alt="Image" src="https://github.com/user-attachments/assets/841ac2d1-9f8f-4885-8e60-d4a15f776e3c" />

---

## 2. O Banco de Registradores (Circuito Principal)

O circuito principal integra os subcomponentes para criar um sistema de memória funcional com múltiplas portas de leitura e uma porta de escrita.

#### Definição Lógica

Este banco de registradores pode armazenar até 8 palavras de 8 bits. Ele permite:
1.  **Escrita (Write):** Gravar um dado de 8 bits em **um** registrador específico.
2.  **Leitura (Read):** Ler o conteúdo de até **dois** registradores simultaneamente e de forma independente.

#### Circuito Simulado

<img width="926" height="481" alt="Image" src="https://github.com/user-attachments/assets/2863d568-415e-4488-b9be-67007f8473a7" />

* **Componentes Utilizados:**
    * 8x **Registrador de 8 Bits**
    * 1x **Demultiplexador 1-para-8** (para controle de escrita)
    * 2x **Multiplexador 8-para-1 (8 bits)** (para controle de leitura)

#### Funcionamento

**Operação de Escrita (Write):**
1.  O dado a ser gravado é colocado no barramento de `ENTRADA` (8 bits).
2.  A `CHAVE` de escrita (3 bits) é configurada com o endereço do registrador de destino (de 0 a 7).
3.  O sinal `LOAD` é ativado (`LOAD = 1`).
4.  No próximo pulso de `CLOCK`, o DEMUX direciona o sinal de habilitação para o registrador selecionado pela `CHAVE`.
5.  Apenas o registrador selecionado armazena o dado presente na `ENTRADA`. Os outros 7 registradores mantêm seu valor inalterado.

**Operação de Leitura (Read):**
1.  Este banco possui duas saídas independentes (`SAÍDA`), cada uma controlada por um MUX 8x1 e sua respectiva `CHAVE` de leitura.
2.  A `CHAVE` do primeiro MUX é configurada com o endereço do primeiro registrador a ser lido.
3.  A `CHAVE` do segundo MUX é configurada com o endereço do segundo registrador a ser lido.
4.  Os multiplexadores selecionam imediatamente os dados dos registradores escolhidos e os apresentam nos barramentos de `SAÍDA`.
5.  **Importante:** A leitura é uma operação combinacional e não depende do `CLOCK`. Os dados de saída são atualizados assim que a chave de seleção é alterada.

#### Análise e Teste de Unidade

O teste envolve a verificação das operações de escrita e leitura.

1.  **Teste de Escrita:**
    * **Objetivo:** Escrever o valor `10101010` no Registrador 5.
    * **Passos:**
        1.  Colocar `10101010` no barramento `ENTRADA`.
        2.  Configurar a `CHAVE` de escrita para `101` (binário para 5).
        3.  Ativar `LOAD = 1`.
        4.  Aplicar um pulso no `CLOCK`.
        5.  Desativar `LOAD = 0`. O dado agora está armazenado.

2.  **Teste de Leitura:**
    * **Objetivo:** Ler o valor do Registrador 5 na primeira `SAÍDA` e do Registrador 2 na segunda `SAÍDA`.
    * **Passos:**
        1.  Configurar a primeira `CHAVE` de leitura para `101` (endereço 5).
        2.  Configurar a segunda `CHAVE` de leitura para `010` (endereço 2).
        3.  Verificar se o barramento da primeira `SAÍDA` exibe `10101010`.
        4.  Verificar o valor no barramento da segunda `SAÍDA` (que deveria ser o que quer que estivesse armazenado no Registrador 2).
