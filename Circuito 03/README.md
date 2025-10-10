###  Porta lógica XOR usando os componentes: AND, NOT, e OR

XOR é a porta que dá 1 só quando A e B são diferentes. Com AND/OR/NOT

---

### Definição Lógica

A tabela verdade de uma porta XOR é a seguinte:

| A | B | Y  |
|:-:|:-:|:---------:|
| 0 | 0 |     0     |
| 0 | 1 |     1     |
| 1 | 0 |     1     |
| 1 | 1 |     0     |

Essa equação combina as entradas usando portas AND, OR e NOT.

---
## Circuito simulado

### Pinos
- **Entradas:** `A`, `B` (1 bit cada, nível lógico 0/1)
- **Saída:** `Y` (1 bit)

### Função lógica
A saída é `1` **somente quando as entradas são diferentes**:  
`Y = A ⊕ B`

### Implementações equivalentes usando AND/OR/NOT
1. **Soma de produtos:**  
   `Y = (A ∧ ¬B) ∨ (¬A ∧ B)`

2. **Máscara do AND:**  
   `Y = (A ∨ B) ∧ ¬(A ∧ B)`

   <img width="587" height="285" alt="image" src="https://github.com/user-attachments/assets/b511a63c-2d23-4631-a8ab-b6b9f50c2d06" />

