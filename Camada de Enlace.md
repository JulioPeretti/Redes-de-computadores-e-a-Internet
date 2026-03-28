# Camada de Enlace
modelo: [Camadas de TCP IP](./Camadas%20de%20TCP%20IP.md)

## Definição
Responsável por transferir datagramas de um nó para o nó adjacente através de um canal de comunicação. É a camada que lida com a interface física e o endereçamento local.

## Características
- **Enquadramento (Framing):** Encapsula o datagrama da camada de rede em um quadro (frame), adicionando cabeçalho e trailer.
- **Acesso ao Meio (MAC):** Protocolos que determinam como os nós compartilham o canal de comunicação (ex: Ethernet, Wi-Fi).
- **Endereço MAC:** Endereço físico único gravado na placa de rede.

## 🛡️ Cybersec Insight
- **ARP Spoofing:** Um atacante envia mensagens ARP falsas para associar seu endereço MAC ao endereço IP de um gateway legítimo, permitindo interceptar o tráfego da rede local (Man-in-the-Middle).
- **MAC Flooding:** Inundar a tabela do switch com endereços MAC falsos para forçá-lo a agir como um hub, facilitando a interceptação de dados.
