# TCP & Telnet - Resumo Rápido

## 1. TCP (Transmission Control Protocol)
**Definição:** Protocolo da Camada de Transporte orientado a conexão, confiável e *byte-stream*.
**Objetivo:** Garantir que os dados cheguem íntegros, na ordem correta e sem duplicidade.

### Estrutura Básica
* **Cabeçalho:** Mínimo de 20 bytes.
* **Campos Chave:** Porta Origem/Destino, Checksum, Flags (SYN, ACK, FIN, RST) e Window Size (controle de fluxo).

### Lógica de Numeração (O Coração do TCP)
Ao contrário do [UDP](./UDP.md), o TCP conta **bytes**, não pacotes.

* **Sequence Number (Seq):**
    * Identifica a posição do **primeiro byte** de dados contido naquele segmento.
    * *Ex:* Se Seq = 1000 e o pacote tem 500 bytes de dados, os bytes são 1000 a 1499.

* **Acknowledgement Number (Ack):**
    * Indica o **próximo byte** que o receptor espera receber.
    * É **cumulativo**: "Ack = 1500" significa "Recebi tudo corretamente até o 1499, mande a partir do 1500".

## 2. Telnet
**Definição:** Protocolo de aplicação (Porta 23) para acesso remoto via terminal (CLI).
**Características:**
* **Texto Plano:** Não usa criptografia (inseguro, substituído pelo SSH).
* **Interatividade:** Tende a enviar cada caractere digitado em um segmento TCP separado (echo remoto), gerando tráfego de pacotes pequenos.
* **Uso Atual:** Debugar portas TCP abertas (ex: `telnet google.com 80`).

## 3. Controle de Fluxo
**Objetivo:** Impedir que o emissor "afogue" o receptor enviando dados mais rápido do que ele consegue processar.

* **Mecanismo:** **Janela Deslizante (Sliding Window)**.
* **Como funciona:**
    * O receptor informa no cabeçalho TCP (campo `Window Size`) quanto espaço livre tem em seu buffer (`rwnd` - Receive Window).
    * O emissor só pode enviar essa quantidade de bytes sem receber um novo `ACK`.
    * **Janela Zero:** Se o buffer enche, o receptor envia `Window = 0`. O emissor para e envia pacotes "probe" periodicamente até liberar espaço.


## 4. Gerenciamento da conexao TCP

### Abertura (3-Way Handshake)
Estabelece a conexão e sincroniza os números de sequência iniciais.
1.  **SYN:** Cliente pede conexão (`Seq=x`).
2.  **SYN-ACK:** Servidor aceita e pede conexão de volta (`Ack=x+1`, `Seq=y`).
3.  **ACK:** Cliente confirma (`Ack=y+1`).
    * *Estado Final:* `ESTABLISHED`.

### Fechamento (4-Way Handshake)
Desconecta de forma graciosa (garante que todos os dados foram entregues).
1.  **FIN:** "A" avisa que terminou de enviar.
2.  **ACK:** "B" confirma o recebimento do FIN.
    * *Nesse momento, a conexão é "half-close" (B ainda pode enviar dados para A).*
3.  **FIN:** "B" avisa que também terminou.
4.  **ACK:** "A" confirma. Conexão encerrada.

# ATAQUE SYN FLOOD: 
Explora uma vulnerabilidade no buffer de conexões pendentes do servidor durante o Handshake.

* **O Ataque:**
    1.  Atacante envia milhares de pacotes **SYN** (frequentemente com IPs falsos/spoofados).
    2.  Servidor responde com **SYN-ACK** e aloca memória para essa "conexão futura".
    3.  Atacante **NÃO** responde com o **ACK** final.
* **Resultado:** O servidor fica com a fila de conexões semi-abertas (*Half-open connections*) cheia, impedindo usuários legítimos de conectar.
* **Contramedida:** **SYN Cookies** (o servidor não aloca memória até receber o ACK final, codificando o estado no próprio número de sequência).


# TCP - Controle de Congestionamento

## O Conceito (vs. Controle de Fluxo)
Enquanto o *Flow Control* protege o **Receptor** (para não estourar o buffer dele), o *Congestion Control* protege a **Rede** (roteadores e links intermediários).
* **Variável Chave:** `cwnd` (Congestion Window).
* **Regra de Ouro:** O emissor envia o **mínimo** entre a janela do receptor (`rwnd`) e a de congestionamento (`cwnd`).

---

## 1. Partida Lenta (Slow Start)
O nome engana. É uma **partida exponencial**.
> [!TIP] Mecânica
> * **Início:** `cwnd` = 1 MSS (Maximum Segment Size).
> * **Crescimento:** A cada `ACK` recebido, aumenta 1 MSS. Na prática, **dobra** a cada RTT (1 ➔ 2 ➔ 4 ➔ 8...).
> * **Gatilho de Parada:** Quando `cwnd` atinge o limiar `ssthresh` (Slow Start Threshold).

## 2. Prevenção de Congestionamento (Congestion Avoidance)
Entra em cena quando a rede já está "cheia" (`cwnd` >= `ssthresh`).
> [!NOTE] AIMD (Additive Increase, Multiplicative Decrease)
> * **Crescimento:** Linear. Aumenta apenas **1 MSS por RTT** inteiro (cautela).
> * **Objetivo:** Sondar o limite da banda sem causar perdas massivas.

---

## 3. Reação a Perdas e Recuperação Rápida

O TCP reage de forma diferente dependendo de *como* ele percebeu a perda:

### Cenário A: Timeout (Grave)
O cronômetro estourou. Silêncio total. A rede deve estar morta.
1. `ssthresh` cai para a metade da `cwnd` atual.
2. `cwnd` é **resetada para 1 MSS**.
3. Reinicia em **Slow Start**.

### Cenário B: 3 ACKs Duplicados (Leve)
A rede ainda respira (outros pacotes estão chegando), só um se perdeu.
* **Fast Retransmit:** Reenvia o pacote perdido imediatamente (sem esperar timeout).
* **Entra em Fast Recovery:**
    1. `ssthresh` cai para a metade.
    2. `cwnd` assume o valor do novo `ssthresh` + 3 (pelos 3 acks recebidos).
    3. **Durante:** Para cada novo Duplicada ACK, aumenta `cwnd` (inflação artificial para manter o fluxo).
    4. **Saída:** Ao chegar um ACK *Novo*, `cwnd` = `ssthresh` e volta para **Congestion Avoidance** (pula o Slow Start).

---
# RESUMO DO CONTROLE DE CONGESTIONAMENTO:

## O Ciclo de Vida da Velocidade (TCP Reno)

1.  **Aceleração (Slow Start):**
    * Pisa fundo. A cada RTT, a velocidade dobra (Exponencial).
    * Vai até bater no teto (`ssthresh`).

2.  **Cruzeiro (Congestion Avoidance):**
    * Passou do teto, pisa leve. Aumenta só um pouquinho por vez (Linear).
    * Está "tateando" o limite máximo da banda.

3.  **A Queda (Reação a Perdas):**
    * **Tropeço (3 ACKs Duplicados):** A rede engasgou.
        * Corta a velocidade pela **metade**.
        * Continua subindo linearmente (Recuperação Rápida).
        * *Visual:* Gráfico Dente de Serra.
    * **Morte (Timeout):** A rede parou.
        * Corta a velocidade para **ZERO** (1 pacote).
        * Reinicia a aceleração exponencial (Slow Start).
