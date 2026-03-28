# TCP (Transmission Control Protocol)

## Definição
Protocolo da Camada de Transporte orientado a conexão, confiável e *byte-stream*. Garante integridade, ordem e ausência de duplicidade.

## Gerenciamento da Conexão
### Abertura (3-Way Handshake)
1. **SYN:** Cliente pede conexão.
2. **SYN-ACK:** Servidor aceita e pede conexão de volta.
3. **ACK:** Cliente confirma.

### Fechamento (4-Way Handshake)
Envolve o envio de flags **FIN** e **ACK** de ambos os lados para garantir que todos os dados foram entregues antes de encerrar.

## Controle de Congestionamento (TCP Reno)
1. **Slow Start:** Aceleração exponencial (dobra a velocidade a cada RTT).
2. **Congestion Avoidance:** Crescimento linear ao atingir o limiar (`ssthresh`).
3. **Reação a Perdas:**
   - **3 ACKs Duplicados:** Corta a velocidade pela metade (Fast Recovery).
   - **Timeout:** Reseta a velocidade para 1 MSS e volta ao Slow Start.

## 🛡️ Cybersec Insight
- **SYN Flood:** Ataque que esgota o buffer do servidor com pedidos de conexão falsos. Contramedida: **SYN Cookies**.
