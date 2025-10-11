# Memória RAM (8 bits)

Este circuito implementa uma **Memória RAM (Random Access Memory)** funcional utilizando **Flip-Flops D**, **demultiplexador** e **multiplexador** para leitura e escrita.  
Possui interface de **8 bits** para dados e sinais de **clock**, **ler**, **escrever** e **chave de endereçamento**.

**Memória RAM**  
<img width="625" height="509" alt="image" src="https://github.com/user-attachments/assets/060d0558-da1b-40cf-8079-5e959c3ee198" />


---

## Componentes Principais

### Registrador (Célula de Memória)
- As células são feitas com **Flip-Flops D**, que armazenam cada bit.
- Cada célula contém **8 FF-D** em paralelo (um **registro de 8 bits**).

  <img width="460" height="433" alt="image" src="https://github.com/user-attachments/assets/2c192ed2-c128-4e4b-b021-37f67e027a44" />


### Demultiplexador 1×8 (1 bit)
- **Direciona o sinal de escrita** para **uma** das 8 células.
- A célula ativa é escolhida pela **chave de endereçamento**.
- Permite escrever na célula selecionada **apenas** se o sinal **escrever** estiver ativo.
- **Obs.:** neste documento, a saída aparece como **8 bits** para simplificar.  
  No circuito principal, a saída do demultiplexador é **dividida via Distribuidor** (nativo do Logisim).

  <img width="443" height="564" alt="image" src="https://github.com/user-attachments/assets/875e3b7c-64e7-46a3-a0cb-e5fc061f1a9d" />


### Multiplexador 8×1 (8 bits)
- **Seleciona** uma das 8 células para **leitura**.
- A célula lida é definida pela **chave de endereçamento**.
- Só transfere dados à saída se o sinal **ler** estiver **ativado**.

  <img width="486" height="348" alt="image" src="https://github.com/user-attachments/assets/5da0df89-3f20-453d-bb29-b754bb39348d" />


**Modo de construção:**  
1. Fazer um **Multiplexador 2×1 de 1 bit**.  
2. A partir dele, construir um **Multiplexador 2×1 de 8 bits** (8 cópias em paralelo).  
3. Em seguida, montar uma **árvore “mata-mata”** com muxes 2×1 (8 bits) controlados por cada bit da chave → **Multiplexador 8×1 (8 bits)**.

   <img width="498" height="429" alt="image" src="https://github.com/user-attachments/assets/ed569988-0d66-4b5b-a947-45ea0618a9e1" />


### Registrador (Cache)
- Um registrador adicional **armazena temporariamente** os dados lidos.
- **Atualiza** apenas quando o sinal **ler** estiver **ativado**.

### Sinais de Controle
- **Clock:** sincroniza todas as operações.
- **Reset:** zera os valores armazenados nas células.
- **Escrever:** ativa a escrita na célula selecionada.
- **Ler:** ativa a leitura da célula selecionada.

---

## Funcionamento Geral

### Escrita de Dados
1. **Entrada de dados:** aplicar os **8 bits** na entrada.
2. **Sinal de controle:** **escrever = 1** para permitir gravação.
3. **Endereçamento:** a chave seleciona **qual célula** receberá os dados.
4. **Demux:** direciona o **sinal de escrita** apenas à célula endereçada.
5. **Armazenamento:** na **próxima borda de clock**, a célula salva o byte de entrada.

### Leitura de Dados
1. **Endereçamento:** a chave escolhe **qual célula** será lida.
2. **Sinal de controle:** **ler = 1** para habilitar a leitura.
3. **Multiplexador:** seleciona os **8 bits** da célula endereçada.
4. **Transferência ao registrador:** os dados vão para o **cache** (registrador).
5. **Saída:** o valor do registrador é enviado à **saída de 8 bits**.

---

## Detalhes do Circuito

### Interface de Entrada
- **Dados (8 bits)** a serem escritos.
- **Endereço (3 bits)** da chave de endereçamento.

### Interface de Controle
- **Clock:** sincroniza o circuito.
- **Escrever:** habilita a escrita na célula endereçada.
- **Ler:** habilita a leitura da célula endereçada.
- **Reset:** zera os registros de memória.

### Interface de Saída
- **Saída (8 bits):** dados lidos da memória (via registrador).

---

## Resumo do Fluxo de Operações

**Escrita:**  
`Dados de entrada → Demux (endereço) → Célula selecionada → (borda do clock) → Armazenado`

**Leitura:**  
`Célula selecionada → Mux 8×1 → Registrador (cache) → Saída`

---

## Vantagens do Circuito
- **Armazenamento dinâmico:** leitura e escrita em tempo real.
- **Endereçamento simples:** seleção por chave de 3 bits.
- **Controle rigoroso:** sinais separados de **ler** e **escrever** evitam conflitos.

---

## Aplicações
- **Memória volátil:** para sistemas com leituras/escritas frequentes.
- **Sistemas embarcados:** pequenas RAMs em dispositivos de baixo custo.
- **Simulação didática:** entender a dinâmica de leitura/escrita em memórias digitais.

---

## Considerações Finais
Este circuito demonstra a implementação de uma **RAM simples** com **FF-D**, **multiplexadores** e **demultiplexadores**, oferecendo um modelo prático para compreender operações fundamentais de **leitura** e **escrita** em sistemas digitais.

