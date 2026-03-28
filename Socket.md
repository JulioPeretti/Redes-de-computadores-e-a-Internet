# Socket API
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## Definição
É a Interface de Programação de Aplicações (API) padrão para comunicação em rede.
- **Não é um protocolo.** É a interface ("Porta") entre a Aplicação e o protocolo de Transporte.
- **Analogia:** O buraco da tomada (Socket) onde você conecta o aparelho.

## Relação com Camadas
- **Cima:** Controlado pela [Camada de Aplicação](./Camada%20de%20Aplicação.md) (Desenvolvedor/Linguagem C/Python).
- **Baixo:** Utiliza serviços da [Camada de Transporte](./Camada%20de%20Transporte.md) (Sistema Operacional).

## Tipos Principais
1. **Stream Sockets (`SOCK_STREAM`):**
    - Usam o protocolo [TCP](./TCP.md).
    - Garante entrega e ordem.
    - Funções Servidor: `socket()` -> `bind()(associa porta)` -> `listen()` -> `accept()`.
    - Funções Cliente: `socket()` -> `connect()`.
2. **Datagram Sockets (`SOCK_DGRAM`):**
    - Usam o protocolo [UDP](./UDP.md).
    - Rápido, sem conexão, sem garantia.
    - Funções: `sendto()` e `recvfrom()`.

## 🛡️ Cybersec Insight
- **Raw Sockets:** Permitem que hackers criem seus próprios cabeçalhos IP/TCP manualmente, ignorando o S.O. (Usado para *IP Spoofing* e scanners como `nmap`).
-
