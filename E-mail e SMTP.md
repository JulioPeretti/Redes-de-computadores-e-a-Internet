camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)
## Estrutura
O sistema de e-mail é composto por 3 partes:
1. **User Agent:** O software do usuário (Outlook, Thunderbird).
2. **Mail Server:** O servidor que armazena e envia (Exchange, Postfix).
3. **Protocolos:** As regras de comunicação.

## SMTP (Simple Mail Transfer Protocol)
- **Função:** Apenas para **ENVIAR** e-mail (Push).
- **Transporte:** Usa [TCP](./TCP.md).
    - Porta `25` (Legado/Servidor-para-Servidor).
    - Porta `587` (Cliente-para-Servidor com TLS).
- **Características:**
    - Protocolo de texto puro (ASCII).
    - Stateful (mantém estado da conversa).
    - Comandos: `HELO`, `MAIL FROM` (Remetente), `RCPT TO` (Destinatário), `DATA` (Corpo), `QUIT`.

## Protocolos de Acesso (Recebimento)
O SMTP não "baixa" e-mail. Para ler, usamos:
- **POP3 (Post Office Protocol):** Modelo "baixa e apaga". Simples e Stateless.
- **IMAP (Internet Mail Access Protocol):** Mantém e-mails no servidor. Sincroniza pastas. Complexo e Stateful.
- **HTTP:** Webmail (Gmail no navegador).

## 🛡️ Cybersec Insight
- **E-mail Spoofing:** O protocolo SMTP original não valida se o remetente é real. Hacker pode enviar como `admin@banco.com`.
    - *Correção:* SPF, DKIM e DMARC (validam o IP do remetente).
- **Phishing:** Uso de engenharia social via e-mail.
- **Open Relay:** Servidor SMTP mal configurado que aceita e reenvia e-mails de qualquer pessoa (usado por Spammers).
