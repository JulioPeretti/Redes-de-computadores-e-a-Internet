# HTTP (HyperText Transfer Protocol)

## Definição
Protocolo responsável pela transferência de hipermídia (texto, imagens, vídeos). É a base da Web.
- **Estado:** Stateless (sem estado). Usa [Cookies](./Cookies.md) para lembrar do usuário.
- **Portas:** 80 (HTTP) e 443 (HTTPS/TLS).

## Evolução
- **HTTP/1.1:** Conexões persistentes (uma conexão para vários objetos).
- **HTTP/2:** Multiplexação (envia arquivos intercalados para evitar bloqueios).

## 🛡️ Cybersec Insight
- **Sniffing:** HTTP puro trafega em texto claro, vulnerável a roubo de senhas via Wireshark.
- **Application Attacks:** Vulnerável a SQL Injection e XSS se as entradas não forem sanitizadas.
