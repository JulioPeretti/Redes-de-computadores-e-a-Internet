# Cookies

## Definição
Pequenos arquivos de texto que os sites salvam no navegador do usuário para manter o **estado** da aplicação.
- **Problema que resolve:** O [HTTP](./HTTP.md) é *stateless* (sem memória). Sem cookies, o servidor esqueceria quem você é assim que você mudasse de página.

## Como Funciona
1. **Criação:** O servidor envia o cabeçalho `Set-Cookie: id=123` na resposta HTTP.
2. **Armazenamento:** O navegador salva esse arquivo no disco do usuário.
3. **Uso:** Em *todas* as requisições futuras para aquele domínio, o navegador envia automaticamente o cabeçalho `Cookie: id=123`.

## Principais Usos
1. **Gerenciamento de Sessão:** Manter login ativo, carrinho de compras, progresso em jogos.
2. **Personalização:** Lembrar preferências (tema escuro, idioma).
3. **Rastreamento:** Monitorar o comportamento do usuário para analytics e anúncios.

## Tipos Importantes
- **Session Cookies:** Temporários. São apagados da memória assim que o navegador fecha.
- **Persistent Cookies:** Possuem data de expiração. Ficam no HD até vencerem ou serem limpos manualmente.
- **Third-Party Cookies:** Criados por domínios externos (ex: Facebook, Google Ads) dentro de outro site. Usados para rastreamento entre sites (Cross-Site Tracking).

## 🛡️ Cybersec Insight
- **Session Hijacking:** O cookie de sessão é a "chave do castelo". Se um atacante roubá-lo (via [XSS](./XSS.md) ou [Wireshark](./Wireshark.md) em HTTP), ele assume a conta da vítima sem precisar da senha.
- **Privacidade:** O uso excessivo de cookies de terceiros levou à criação de leis como a LGPD/GDPR e ao bloqueio nativo em navegadores modernos.
