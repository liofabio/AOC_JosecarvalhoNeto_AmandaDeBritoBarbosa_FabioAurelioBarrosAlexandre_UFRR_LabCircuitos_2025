# Detector de Sequência 101

Este circuito detecta o padrão binário **101** em um fluxo de bits de entrada.  
Utiliza portas lógicas básicas para verificar e sinalizar quando essa sequência ocorre.

<img width="472" height="277" alt="image" src="https://github.com/user-attachments/assets/90756188-395c-4e47-9b49-9d3a403698e2" />

---

## Descrição Geral

### Entradas
- **Fluxo de bits:** um conjunto de bits binários é aplicado na entrada.
- Cada bit é analisado individualmente para verificar a presença da sequência **101**.

### Saída
- **Um único bit** que fica ativo (**1**) quando a sequência **101** é detectada.
- Permanece inativo (**0**) nos demais casos.

---

## Componentes Utilizados

### Portas Lógicas
- **AND:** verifica quando dois ou mais sinais satisfazem a condição requerida.
- **NOT:** inverte o valor de um bit, permitindo validar o **0** da sequência.
- **OR:** combina resultados parciais de portas AND.

### Conexões
- Os bits de entrada são ligados a combinações de portas lógicas para validar cada posição da sequência (**1**, **0**, **1**).

---

## Funcionamento do Circuito

### Sequência Detectada
Para reconhecer **101**, as condições são:
1. O **primeiro bit** deve ser **1**.  
2. O **segundo bit** deve ser **0**.  
3. O **terceiro bit** deve ser **1**.

### Processo de Detecção
- **Bit 1:** passa diretamente por uma porta **AND** para validar o valor **1**.  
- **Bit 2:** é invertido por uma porta **NOT** para validar que seja **0**.  
- **Bit 3:** passa diretamente por outra entrada de **AND** para validar o valor **1**.

**Combinação final:**  
As portas **AND** combinam os três bits consecutivos (**1**, **0**, **1**).  
Se as condições forem atendidas, a saída da **AND** resulta em **1**, que é enviada para a saída principal.

---

## Casos de Teste

| Entrada   | Saída |
|-----------|:-----:|
| `000`     |   0   |
| `101`     |   1   |
| `110`     |   0   |
| `01010101`|   1   | <!-- para cada ocorrência de 101 -->

---

## Aplicações do Detector de Sequência
- **Comunicação Digital:** identificação de padrões específicos em fluxos de dados.  
- **Controladores de Estado Finito:** monitoramento de eventos em sistemas digitais.  
- **Filtros de Sinal:** extração de informações relevantes de sequências binárias.



