# Cookies

## Definição
Pequenos arquivos de texto salvos no navegador para manter o **estado** da aplicação.
- **Problema:** HTTP é *stateless*. Sem cookies, o servidor não lembraria do usuário entre requisições.

## Como Funciona
1. **Criação:** Servidor envia `Set-Cookie: id=123`.
2. **Armazenamento:** Navegador salva no disco.
3. **Uso:** Navegador envia `Cookie: id=123` em todas as requisições futuras para aquele domínio.

## 🛡️ Cybersec Insight
- **Session Hijacking:** Se um atacante rouba o cookie de sessão (via XSS ou Wireshark), ele assume a conta da vítima.
- **Privacidade:** Cookies de terceiros (Third-Party) levaram à criação de leis como LGPD/GDPR.
