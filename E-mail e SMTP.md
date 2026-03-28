# E-mail e SMTP

## SMTP (Simple Mail Transfer Protocol)
- **Função:** Apenas para **ENVIAR** e-mail (Push).
- **Transporte:** TCP (Portas 25 ou 587 com TLS).
- **Características:** Texto puro (ASCII), Stateful.

## Protocolos de Recebimento
- **POP3:** Modelo "baixa e apaga".
- **IMAP:** Sincroniza pastas, mantém no servidor.

## 🛡️ Cybersec Insight
- **E-mail Spoofing:** SMTP original não valida remetente. Correção: SPF, DKIM e DMARC.
- **Open Relay:** Servidor mal configurado usado por spammers.
