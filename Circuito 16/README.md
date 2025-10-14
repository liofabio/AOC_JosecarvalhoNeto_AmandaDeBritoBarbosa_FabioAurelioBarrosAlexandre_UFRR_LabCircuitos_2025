# Decodificador BCD para Display de 7 Segmentos

Este relatório descreve a estrutura, a lógica booleana e o funcionamento de um circuito decodificador. A função deste circuito é converter um número em formato BCD (Binary Coded Decimal) de 4 bits para o formato de controle de um display de 7 segmentos, permitindo a exibição de dígitos decimais (0 a 9).

---

## 1. O Display de 7 Segmentos

Antes de analisar o decodificador, é importante entender o componente que ele controla.

#### Definição

O display de 7 segmentos é um dispositivo de exibição eletrônico composto por sete LEDs individuais, dispostos em forma de um "8". Cada LED é chamado de "segmento" e identificado por uma letra de 'a' a 'g'. Ao acender combinações específicas de segmentos, é possível formar os dígitos de 0 a 9 e alguns caracteres.

Existem dois tipos principais:
* **Catodo Comum:** Todos os catodos (terminais negativos) dos LEDs são conectados juntos a um pino comum, que é ligado ao terra (GND). O decodificador deve fornecer um sinal de nível lógico **alto (1)** para acender um segmento.
* **Anodo Comum:** Todos os anodos (terminais positivos) dos LEDs são conectados a um pino comum, que é ligado à alimentação (VCC). O decodificador deve fornecer um sinal de nível lógico **baixo (0)** para acender um segmento.

O circuito analisado foi projetado para um display do tipo **Catodo Comum**.

---

## 2. Decodificador BCD para 7 Segmentos

Este é o circuito principal, responsável pela "tradução" do código binário para o padrão do display.

#### Definição Lógica

O circuito é um bloco puramente combinacional. Ele recebe 4 bits de entrada (A, B, C, D), que representam um número BCD de 0 (0000) a 9 (1001), e produz 7 saídas (a, b, c, d, e, f, g), uma para cada segmento do display.

**Tabela Verdade:**

A tabela a seguir mostra qual segmento deve ser aceso (saída 1) para cada entrada BCD.

| Decimal | D | C | B | A |  | a | b | c | d | e | f | g |
|:---:|:-:|:-:|:-:|:-:|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **0** | 0 | 0 | 0 | 0 |  | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| **1** | 0 | 0 | 0 | 1 |  | 0 | 1 | 1 | 0 | 0 | 0 | 0 |
| **2** | 0 | 0 | 1 | 0 |  | 1 | 1 | 0 | 1 | 1 | 0 | 1 |
| **3** | 0 | 0 | 1 | 1 |  | 1 | 1 | 1 | 1 | 0 | 0 | 1 |
| **4** | 0 | 1 | 0 | 0 |  | 0 | 1 | 1 | 0 | 0 | 1 | 1 |
| **5** | 0 | 1 | 0 | 1 |  | 1 | 0 | 1 | 1 | 0 | 1 | 1 |
| **6** | 0 | 1 | 1 | 0 |  | 1 | 0 | 1 | 1 | 1 | 1 | 1 |
| **7** | 0 | 1 | 1 | 1 |  | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| **8** | 1 | 0 | 0 | 0 |  | 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| **9** | 1 | 0 | 0 | 1 |  | 1 | 1 | 1 | 1 | 0 | 1 | 1 |

#### Circuito Simulado 

<img width="479" height="586" alt="Image" src="https://github.com/user-attachments/assets/8153db82-f86f-4dab-ac2a-e00e597c2e42" />

* **Componentes Utilizados:**
    * Portas **AND**
    * Portas **OR**
    * Portas **NOT** (Inversores)
    * Portas **XOR** / **XNOR**

* **Funções Lógicas:**
  A partir da tabela verdade, é possível derivar a equação booleana simplificada para cada segmento. As expressões a seguir são as implementações padrão para um decodificador BCD:

  $$ a = A + C + (B \land D) + (\neg B \land \neg D) $$
  $$ b = \neg B + (\neg C \land \neg D) + (C \land D) $$
  $$ c = B + \neg C + D $$
  $$ d = (\neg B \land \neg D) + (C \land \neg D) + (\neg B \land C) + (B \land \neg C \land D) $$
  $$ e = (\neg B \land \neg D) + (C \land \neg D) $$
  $$ f = A + (\neg C \land \neg D) + (B \land \neg C) + (B \land \neg D) $$
  $$ g = A + (B \land \neg C) + (\neg B \land C) + (C \land \neg D) $$

  O circuito na imagem implementa essas funções lógicas através de uma rede de portas para gerar as sete saídas de controle.

#### Análise e Teste de Unidade

Como o circuito é combinacional, o teste consiste em aplicar todas as combinações de entrada válidas e verificar se as saídas correspondem à tabela verdade.

1.  **Configurar a Entrada:** Aplique um valor BCD nas entradas A, B, C, D. Por exemplo, para exibir o número **5**, a entrada deve ser `D=0`, `C=1`, `B=0`, `A=1`.
2.  **Observar as Saídas:** Verifique o estado lógico das sete saídas (a-g). Para a entrada `0101`, as saídas esperadas são:
    * `a=1`, `b=0`, `c=1`, `d=1`, `e=0`, `f=1`, `g=1`.
3.  **Verificar o Display:** Confirme que os segmentos acesos no display formam corretamente o dígito `5`.
4.  **Repetir o Processo:** Repita os passos para todos os outros dígitos de 0 a 9 para garantir a funcionalidade completa do decodificador.
5.  **Teste de Entradas Inválidas:** (Opcional) Aplique uma entrada binária maior que 9 (de 1010 a 1111). O display deve mostrar um padrão não numérico ou apagar, dependendo da lógica de implementação para esses casos.
