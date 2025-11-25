# 🎮 Jogo da Velha em Assembly MIPS

Este é um jogo simples de **Jogo da Velha (Tic-Tac-Toe)** implementado em linguagem Assembly para arquitetura MIPS. Ele é projetado para ser executado em um simulador MIPS, como o **MARS**.

---

## ✨ Funcionalidades

* **Dois Jogadores:** Permite que dois jogadores ('X' e 'O') se alternem.
* **Tabuleiro Interativo:** O jogador insere a posição desejada (de 1 a 9).
* **Verificação de Vitória:** Detecta quando um jogador completa uma linha, coluna ou diagonal.
* **Verificação de Empate:** Detecta a condição de "velha".

---

## 🛠️ Como Executar

1.  **Requisito:** Você precisa de um simulador MIPS (ex: **QtSpim** ou **MARS**).
2.  **Carregar o Código:** Copie o código Assembly e carregue-o no simulador.
3.  **Executar:** Inicie a execução a partir do rótulo `main`.
4.  **Jogar:** Siga as instruções no console, inserindo um número de **1 a 9** quando solicitado, que corresponde à posição no tabuleiro.

### 🗺️ Mapeamento do Tabuleiro

O tabuleiro é mapeado da seguinte forma, onde cada número representa a posição que o jogador deve digitar:

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |
| 7 | 8 | 9 |

---

## 💻 Estrutura do Código

### 💾 Seção de Dados (`.data`)

| Rótulo | Descrição |
| :--- | :--- |
| `tabuleiro` | `BYTE[9]`. Armazena o estado real (0=vazio, 1='X', 2='O'). |
| `exibicao` | `BYTE[9]`. Armazena caracteres para display ('1'-'9' ou 'X'/'O'). |
| `msg_...` | Strings de texto para interação com o usuário (início, jogador, vitória, empate, etc.). |

### 🧠 Registradores Chave

Os registradores `$s0` e `$s1` são usados para controlar o estado do jogo:

| Registrador | Uso no Loop Principal (`main`) |
| :--- | :--- |
| `$s0` | **Jogador Atual**: 1 para 'X', 2 para 'O'. |
| `$s1` | **Contador de Jogadas**: De 0 a 9. Usado para verificar empate. |

### ⚙️ Lógica de Alternância

A troca de jogador é realizada usando a operação lógica **XOR** na instrução:

```assembly
xori $s0, $s0, 3 
# Se $s0=1 (X), torna-se 2 (O). Se $s0=2 (O), torna-se 1 (X).
