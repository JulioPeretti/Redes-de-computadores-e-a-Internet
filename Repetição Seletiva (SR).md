# Repetição Seletiva (SR)

## O Problema do GBN
O protocolo [Go-Back-N](./Go-Back-N.md) sofre de problemas de performance quando há muitos erros na rede.
- **Cenário:** Se a janela é de 1000 pacotes e o pacote 2 se perde, o GBN retransmite do 2 ao 1000 (999 pacotes inúteis retransmitidos).
- **Solução:** A **Repetição Seletiva** evita retransmissões desnecessárias reenviando *apenas* os pacotes que suspeita-se terem sido perdidos ou corrompidos.


## ==**Diferenças Chave: GBN vs SR**==

| Característica         | Go-Back-N (GBN)                                    | Repetição Seletiva (SR)                                         |
| :--------------------- | :------------------------------------------------- | :-------------------------------------------------------------- |
| **Buffer no Receptor** | **Não.** Descarta pacotes fora de ordem.           | **Sim.** Armazena pacotes fora de ordem até preencher a lacuna. |
| **Tipo de ACK** | **Cumulativo** (ACK 5 confirma tudo até o 5).      | **Individual** (ACK 5 confirma apenas o 5).                     |
| **Temporizadores** | Um único timer para o pacote mais antigo (`base`). | Um timer lógico para **cada** pacote não confirmado.            |
| **Retransmissão** | Janela inteira (`base` até `next`).                | Apenas o pacote cujo timer estourou.                            |

## Mecanismo Detalhado

### 1. O Remetente (Sender)
- **Janela:** Mantém a janela de tamanho $N$.
- **Envio:** Envia pacotes dentro da janela.
- **Timeout:** Cada pacote tem seu próprio timer. Se o timer do pacote `X` estoura, ele reenvia **apenas o pacote `X`**.
- **Recebimento de ACK:**
    - Se receber ACK do `base`, a janela desliza.
    - Se receber ACK de um pacote no meio da janela, apenas marca aquele pacote como "recebido", mas a janela **não anda** até o `base` ser confirmado.

### 2. O Destinatário (Receiver)
Diferente do GBN, ele aceita pacotes fora de ordem.
- **Pacote Esperado:** Entrega para a camada de aplicação e desliza a janela.
- **Pacote Fora de Ordem:**
    - Envia **ACK** imediato.
    - **Armazena no Buffer** (não entrega para a aplicação ainda).
    - Espera o pacote faltante chegar. Quando a lacuna é preenchida, entrega o lote inteiro em ordem para a aplicação.

## O Dilema da Janela (Window Size Dilemma)
Existe uma regra matemática crítica para o SR funcionar.
- O tamanho da janela ($N$) deve ser menor ou igual à metade do espaço de números de sequência.
- **Fórmula:** $N \le \frac{\text{Espaço de Sequência}}{2}$.
- **Por que?** Se a janela for muito grande (ex: Sequência 0, 1, 2, 3 e Janela de tamanho 3), o receptor não consegue distinguir se o pacote "0" que chegou é um **novo pacote** (da próxima rodada) ou uma **retransmissão** do pacote antigo (porque o ACK se perdeu).


## Esquema:

> **Nota Prática:** O [TCP](./TCP.md) moderno usa uma mistura híbrida: ele usa ACKs cumulativos (como GBN) mas pode fazer buffer de segmentos fora de ordem e usar SACK (Selective ACK) para otimizar (como SR).
