# UDP (User Datagram Protocol)
camada: [Camada de Transporte](./Camada%20de%20Transporte.md)

## Definição
Protocolo não orientado a conexão (sem Handshake). É rápido e leve, ideal para aplicações de tempo real e [DNS](./DNS.md).

## Características
- **Sem estados de conexão:** Não possui buffers de controle de congestionamento, sendo eficiente para muitas conexões simultâneas.
- **Cabeçalho Pequeno:** Apenas 8 bytes (contra 20 bytes do TCP).
- **Soma de Verificação (Checksum):** Identifica se bits foram alterados, mas apenas descarta o pacote em caso de erro.
