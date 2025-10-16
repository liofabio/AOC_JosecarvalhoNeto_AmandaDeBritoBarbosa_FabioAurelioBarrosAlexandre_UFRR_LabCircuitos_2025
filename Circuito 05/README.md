# Memória ROM de 8 bits

## Definição

Uma memória ROM é um tipo de memória não volátil (não pode ser alterada por um usuário comum) usada principalmente em BIOS de computadores, cartuchos de videogames e em dispositivos móveis.
Ela usada para armazenar dados e instruções essenciais e permanentes, que são necessários para inicializção do hardware, iniciar a sequência de boot e carregar o sistema opercaional de um dispostivo.  

O circuito de memória proposto tem organização de 8 palavras de 8 bits (8x8), utilizando portas lógicas OR, AND, inversores, pinos de entrada e barramento de 8 bits na saída.
<img width="1240" height="862" alt="Image" src="https://github.com/user-attachments/assets/75b1e4cf-d02c-4c2e-b4b5-4569cdceecb3" />
## Funcionamento
A memória proposta pode ser decomposta em:
- Decodificador de Endereços: responsável por selecionar qual palavra de memória será lida;
- Matriz de Memória: onde os dados são efetivamente armazenado através de conexões físicas;
- Lógica de Saída: responsável por agrupar os bits da palabra selecionada e apresentá-los;

**1. Entradas de Endereçamento**  
As linhas de endereço são representads pelas entradas A2, A1 e A0. Com 3 bits de endereço, é possível acessar 2^3 = 8 localizações de memória distintas, variando do endereço 0 (000) ao endereço 7 (111).

**2. Decodificador de Endereços**
Composto por:  
- 3 portas NOT, uma linha para cada endereço gerando sinais inversos complementares;
- 8 portas AND, cada uma conectada a uma combinação únicas das linhas de endereço;

**3. Matriz de Memória e Lógica de Saída**
Composto por 8 portas OR. A saída de cada porta OR corresponde a um bit da palavra de dados de 8 bits na saída final (D7 a D0).

--- 

# Exemplo de Funcionamento
O contexto para exemplificação será a BIOS de inicialização de um computador.
Considerando `LOAD_A #val` como uma instrução que carrega um valor de 4 bits no registrador A.

1. Ao ligar o computador, o endereço da CPU sempre inicia no `000`. O processador coloca esse endereço na suas linhas de endereço.
2. A ROM recebe `000` das entradas e a porta correspondende (AND 0) é ativada. As conexões dessa porta AND ativam as saídas correspondentes, colocando o valor `11001010` no barramento de dados.
3. O processador lê o valor e decodifica, interpretando a instrução `LOAD_A #val` representada pelo número binário trazido da ROM, posteriormente executando a instrução. Agora, o registrador A contém o valor 8.
4. O processador avança o ponteiro de instrução para o próximo endereço: `001`.
5. Esses passos seguem da mesma forma: a CPU continua pedindo à ROM o contéudo dos endereços, enquanto a ROM entrega as palavras de 8 bits, até que a CPU encontre uma instrução que pare ou pule para outro programa.
<img width="1247" height="907" alt="Image" src="https://github.com/user-attachments/assets/7a2a170d-5324-4665-a049-1e6accffd027" />
