# DNS (Domain Name System)
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## Definição
É o diretório da internet. Traduz **Hostnames** amigáveis (ex: `google.com`) para **Endereços IP** (ex: `142.250.1.1`).

## Transporte
- **Protocolo Principal:** Usa [UDP](./UDP.md) (Porta 53) para consultas rápidas (pois o overhead do TCP seria lento demais).
- **Fallback:** Usa [TCP](./TCP.md) (Porta 53) apenas se a resposta for muito grande ou para Transferência de Zona entre servidores.

## Hierarquia
1. **Root Servers (Raiz):** O topo. Sabem quem cuida dos TLDs.
2. **TLD Servers (Top-Level Domain):** Cuidam dos domínios `.com`, `.org`, `.br`.
3. **Authoritative Servers (Autoritativos):** O servidor final da organização que tem o mapeamento real.
4. **Local DNS (LDNS):** O servidor do provedor (ISP) ou público (8.8.8.8) que faz a busca para o usuário.

## Tipos de Consulta
- **Recursiva:** O cliente joga a responsabilidade para o LDNS ("Me dê a resposta final").
- **Iterativa:** O LDNS pergunta passo a passo na hierarquia ("Me dê a próxima dica").

## Principais Registros (Records)
- **A:** Hostname $\to$ IPv4.
- **AAAA:** Hostname $\to$ IPv6.
- **CNAME:** Apelido (Alias) $\to$ Nome Real (Canonical).
- **NS:** Domínio $\to$ Servidor DNS Autoritativo.
- **MX:** Domínio $\to$ Servidor de E-mail.

## 🛡️ Cybersec Insight
- **DNS Cache Poisoning:** Um atacante injeta uma resposta falsa no cache do LDNS, redirecionando usuários para um site de phishing (ex: banco falso).
- **DNS Amplification (DDoS):** Hacker usa "Open Resolvers" para enviar pequenas perguntas (com IP da vítima spoofado) e o servidor responde com pacotes gigantes para a vítima.
- **DNS Tunneling:** Passar dados (exfiltração) ou comandos C&C escondidos dentro de consultas DNS para furar Firewalls.
