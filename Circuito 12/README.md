# Máquina de Estado

O circuito é um modelo matemático usado para representar e controlar sistemas que podem estar em um **número finito de estados** distintos.  
A transição entre estados ocorre com base em **entradas** e/ou **eventos externos**.  
É amplamente utilizado em **sistemas digitais**, **controle automático**, **programação** e outros domínios.

**Máquina de Estado**  
<img width="410" height="253" alt="image" src="https://github.com/user-attachments/assets/43ae77c5-5186-4a00-a811-4cb2bffade45" />


---

## Componentes do Circuito

### Entrada (ENTRADA)
- Representa o sinal externo que influencia o comportamento da máquina de estado.
- Pode assumir valores binários (0 ou 1) para condicionar a lógica do circuito.

### Clock (CLOCK)
- Sincroniza as transições de estado no Flip-Flop D.
- Mudanças de estado ocorrem apenas nas bordas do clock, garantindo operação síncrona.

### Flip-Flop D
- Elemento de memória que armazena o **estado atual** da máquina.
- A entrada **D** recebe o **próximo estado** calculado pela lógica combinacional.
- A saída do FF fornece o **estado atual** para a lógica combinacional.

  <img width="221" height="138" alt="image" src="https://github.com/user-attachments/assets/be6bb5a4-845d-4695-826c-a148196a1ac1" />


### Lógica Combinacional
- Composta por portas **AND**, **OR** e **NOT**.
- **Calcula o próximo estado** a partir da entrada e do estado atual.
- **Determina a saída** com base no estado atual e/ou na entrada.

### Saída (SAÍDA)
- Representa o resultado da máquina de estado, podendo ativar ou controlar outros sistemas.

---

## Funcionamento do Circuito

### Estado Atual
- O Flip-Flop D mantém o estado atual, atualizado a cada ciclo de clock.

### Cálculo do Próximo Estado
- A lógica combinacional processa o **estado atual** e a **entrada** para determinar o **próximo estado**, que é aplicado à entrada **D**.

### Saída do Circuito
- A saída é gerada pela lógica combinacional.
- Pode depender apenas do **estado atual** (**FSM de Moore**) ou do **estado** e da **entrada** (**FSM de Mealy**).

---

## Aplicações Possíveis
- **Controle de Semáforo:** cada estado representa uma luz (vermelho, amarelo, verde), com transições condicionadas pela entrada.
- **Contadores Sequenciais:** contagem/seqüenciamento de estados de forma síncrona.
- **Sistemas de Controle:** implementação de lógicas de controle em máquinas industriais e automação.


