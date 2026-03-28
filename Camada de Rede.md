# Camada de Rede
modelo: [Camadas de TCP IP](./Camadas%20de%20TCP%20IP.md)

## Definição
Responsável por mover pacotes da origem ao destino através de redes interconectadas. Diferente da camada de transporte, que foca na comunicação processo-a-processo, a camada de rede foca na comunicação hospedeiro-a-hospedeiro.

## Funções Principais
- **Roteamento:** Determinar a rota percorrida pelos pacotes da origem ao destino (algoritmos de roteamento).
- **Repasse (Forwarding):** Mover pacotes da entrada do roteador para a saída apropriada.

## Protocolos e Conceitos
- **IP (Internet Protocol):** O principal protocolo desta camada.
- **Endereçamento:** Atribuição de endereços únicos (IPv4 e IPv6) para interfaces de rede.
- **ICMP:** Usado para envio de mensagens de erro e informações operacionais (ex: ping).

## 🛡️ Cybersec Insight
- **IP Spoofing:** Técnica de falsificação do endereço IP de origem para mascarar a identidade do atacante ou realizar ataques de negação de serviço.
- **Fragmentação de IP:** Atacantes podem usar pacotes fragmentados de forma maliciosa para tentar burlar sistemas de detecção de intrusão (IDS).
