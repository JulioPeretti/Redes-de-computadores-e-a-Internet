# DNS (Domain Name System)

## Definição
Traduz **Hostnames** (google.com) para **Endereços IP** (142.250.1.1).

## Transporte
- **UDP (Porta 53):** Consultas rápidas.
- **TCP (Porta 53):** Respostas grandes ou transferência de zona.

## Hierarquia
1. **Root Servers:** Topo da hierarquia.
2. **TLD Servers:** Cuidam de `.com`, `.org`, `.br`.
3. **Authoritative Servers:** Servidores finais com o mapeamento real.

## 🛡️ Cybersec Insight
- **DNS Cache Poisoning:** Injeção de resposta falsa para redirecionar usuários.
- **DNS Amplification (DDoS):** Uso de reflexão para inundar a vítima com pacotes grandes.
- **DNS Tunneling:** Exfiltração de dados escondidos em consultas DNS.
