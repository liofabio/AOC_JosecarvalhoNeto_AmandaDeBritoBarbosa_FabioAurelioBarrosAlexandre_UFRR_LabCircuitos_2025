# Memória RAM (8 bits)

Uma **RAM de 8 bits** feita com **Flip-Flops D**, **Demultiplexador** (para escrita) e **Multiplexador** (para leitura).  
Interface: dados de **8 bits**, endereço de **3 bits** (8 células), controle por **clock**, **ler**, **escrever** e **reset**.

---

## Visão Geral
- **Célula de memória (8 bits)**: 8 Flip-Flops D em paralelo formam 1 registrador de 8 bits.
- **Banco de 8 células**: endereçadas por uma chave de 3 bits (`A2 A1 A0`).
- **Demux 1→8 (escrita)**: direciona o pulso de escrita apenas para a célula selecionada.
- **Mux 8→1 (8 bits)**: seleciona qual célula vai para a saída durante a leitura.
- **Registrador de saída (cache, opcional)**: armazena o dado lido quando `ler=1` antes de expor na saída.


---

## Pinos / Interfaces
**Entradas**
- `D[7:0]` — Dados de entrada (para escrita).
- `A[2:0]` — Endereço (seleciona 1 entre 8 células).
- `CLK` — Clock (sincroniza escrita e, opcionalmente, o registrador de saída).
- `WE` — *Write Enable* (1 = escreve).
- `RE` — *Read Enable* (1 = lê).
- `RST` — Reset (zera Flip-Flops D).


---

## Funcionamento

### Escrita
1. **Endereço**: `A` seleciona a célula-alvo.  
2. **Demux**: habilita **somente** o `WE` da célula endereçada.  
3. **Captura**: na **borda ativa** de `CLK`, a célula salva `D[7:0]` (se `WE=1`).  

**Fluxo**: `D[7:0]` → Demux (via `A`, `WE`) → Flip-Flops D da célula → armazenado em `CLK`.

### Leitura
1. **Endereço**: `A` escolhe a célula-fonte.  
2. **Mux**: roteia a palavra de 8 bits da célula selecionada.  
3. **Registrador (opcional)**: se `RE=1`, atualiza o cache na borda de `CLK` e expõe em `Q`.

**Fluxo**: Célula endereçada → Mux 8→1 → (Registrador se houver `RE`) → `Q[7:0]`.

---

## Tabela de Operações
| `WE` | `RE` | Ação                               | Efeito nos dados                |
|:----:|:----:|------------------------------------|---------------------------------|
|  1   |  0   | **Escrita** na célula `A`          | `mem[A] ← D` (na borda de `CLK`)|
|  0   |  1   | **Leitura** da célula `A`          | `Q ← mem[A]` (direto ou via reg)|
|  1   |  1   | Evitar                              | Pode causar conflito de intenção|
|  0   |  0   | Ocioso                              | Sem mudança; saída mantém estado|

> Se usar registrador de saída **sincronizado**, `Q` muda apenas em borda de `CLK` com `RE=1`.  
> Com saída **combinacional** (sem registrador), `Q` segue o Mux imediatamente.

---

## Construção dos Blocos

### 1) Célula (Registrador 8 bits)
- 8× Flip-Flop D (com `CLK` e `RST` compartilhados).
- Entrada paralela `D[7:0]` — habilitada pela linha de escrita local (do Demux).

### 2) Demultiplexador 1→8 (habilitação de escrita)
- Entradas: `WE`, `A[2:0]`.
- Saídas: `WE_0 … WE_7` (somente a correspondente ao endereço vai a 1).
- **No Logisim**: pode usar **Decoder** (`3→8`) + `AND(WE, sel[i])` ou um **Demux** nativo.  
- **Distribuidor**: para replicar `WE` e levar às células.

### 3) Multiplexador 8→1 (largura 8 bits)
- **Abordagem hierárquica**:
  1. **Mux 2→1 (1 bit)** — bloco base.
  2. **Mux 2→1 (8 bits)** — 8 cópias do bloco de 1 bit em paralelo.
  3. **Árvore “mata-mata”**: combine 2→1 (8 bits) em estágios até formar um **8→1 (8 bits)**.
- Seleção por `A[2:0]`.


---


