# Socket API
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## Definição
É a Interface de Programação de Aplicações (API) padrão para comunicação em rede. Não é um protocolo, mas a interface ("porta") entre a Aplicação e o Transporte.

## Tipos Principais
1. **Stream Sockets (SOCK_STREAM):** Usam o protocolo [TCP](./TCP.md). Garantem entrega e ordem.
2. **Datagram Sockets (SOCK_DGRAM):** Usam o protocolo [UDP](./UDP.md). São rápidos e sem conexão.

## 🛡️ Cybersec Insight
- **Raw Sockets:** Permitem criar cabeçalhos manuais (IP/TCP), ignorando o S.O. Usado para IP Spoofing e scanners como o nmap.
- **Buffer Overflow:** Se um programa em C ler dados do socket sem limitar o tamanho, pode permitir execução remota de código.
