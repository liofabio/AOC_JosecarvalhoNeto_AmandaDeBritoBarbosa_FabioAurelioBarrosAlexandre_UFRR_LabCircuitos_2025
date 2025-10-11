# Explicação dos Circuitos com Mapa de Karnaugh

O objetivo deste documento é mostrar **por que dois circuitos diferentes produzem a mesma saída**, usando o **Mapa de Karnaugh** para simplificar a expressão booleana do circuito original e validá-la contra um circuito simplificado.

**Circuito simplificado**  
<img width="548" height="293" alt="image" src="https://github.com/user-attachments/assets/86c8632f-fd94-41bf-bf81-61349afa9edc" />


---

## Circuito Original (Não Simplificado)

Expressão booleana dada:

S = A'B'C + ABC' + A'BC' + ABC

---

## Montagem do Mapa de Karnaugh (3 variáveis: A, B, C)

Para três variáveis existem **8 células** (todas as combinações de A, B, C).  
Preenchimento a partir dos mintermos:

- `A'B'C`  → (A=0, B=0, C=1)  
- `ABC'`   → (A=1, B=1, C=0)  
- `A'BC'`  → (A=0, B=1, C=0)  
- `ABC`    → (A=1, B=1, C=1)

Mapa (AB em ordem Gray: 00, 01, 11, 10):

| AB \ C | 0 | 1 |
|:------:|:-:|:-:|
| **00** | 0 | 1 |
| **01** | 1 | 0 |
| **11** | 1 | 1 |
| **10** | 0 | 0 |

---

## Simplificação pelo Karnaugh

### Agrupamentos válidos
1. **Par em C=0**: células (01, 0) e (11, 0) → elimina A  
⇒ B · C'

markdown
Copiar código
2. **Par em AB=11**: células (11, 0) e (11, 1) → elimina C  
⇒ A · B

markdown
Copiar código
3. **Célula isolada (00, 1)**: não tem adjacente 1 para agrupar  
⇒ A' · B' · C

shell
Copiar código

### Expressão simplificada
Combinando os implicantes:

S = B·C' + A·B + A'·B'·C

yaml
Copiar código

> Observação: a forma acima é **equivalente** à expressão original e resulta do agrupamento
> mais econômico possível dado o preenchimento do mapa.

---

## Comparação dos Circuitos

- **Circuito não simplificado**  
  Implementa a soma completa:  
  `S = A'B'C + ABC' + A'BC' + ABC`  
  (mais portas e interconexões).

- **Circuito simplificado**  
  Implementa a forma reduzida:  
  `S = B·C' + A·B + A'·B'·C`  
  (menos portas, mesmo comportamento).

### Saída
Ambas as realizações geram **exatamente a mesma saída S** para todas as combinações de A, B, C.

---

## Conclusão
O uso do **Mapa de Karnaugh** reduz o número de componentes necessários, mantendo o comportamento funcional **idêntico**.  
Isso resulta em um circuito **mais eficiente** e **mais fácil de implementar/manter**.
