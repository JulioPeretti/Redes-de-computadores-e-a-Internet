# Redes-de-computadores-e-a-Internet
Jim Kurose e Keith W. Ross, Top Down, 8ª Edição.

Este repositório contém meus estudos e anotações detalhadas baseadas na literatura de Redes de Computadores (Modelo OSI/TCP-IP). O foco aqui é entender a comunicação fim-a-fim e o roteamento de pacotes, sendo esses fundamentos da área da **Segurança da Informação**. 

O enfoque do estudo foi nas seguintes camadas:

### 1. Camada de Aplicação (Application Layer)
Onde os processos de rede encontram as aplicações. Estudo dos protocolos que permitem a interface direta com o usuário.
* **Protocolos:** HTTP/HTTPS, DNS, FTP, SMTP e SSH.
* **Segurança:** Foco em ataques de aplicação (ex: DNS Spoofing, Interceptação de tráfego HTTP).
* **Portas Comuns:** 80, 443, 53, 22.

### 2. Camada de Transporte (Transport Layer)
Responsável pela comunicação lógica entre processos em diferentes hosts.
* **TCP (Transmission Control Protocol):** Orientado à conexão, controle de fluxo e congestionamento (Three-way handshake).
* **UDP (User Datagram Protocol):** Sem conexão, baixa latência (Streaming, DNS).
* **Conceito Chave:** Multiplexação e Demultiplexação via portas.

### 3. Camada de Rede (Network Layer)
Responsável por mover pacotes da origem ao destino através de redes interconectadas.
* **Protocolos:** IPv4, IPv6 e ICMP.
* **Roteamento:** Algoritmos de vetor de distância vs. estado de enlace.
* **Fragmentação:** Como os datagramas são divididos para respeitar o MTU.

---

## Origem do resumo:
As notas foram exportadas diretamente do meu **Obsidian** e organizadas para facilitar a revisão de conceitos de protocolos e estruturas de pacotes.
