# HTTP (HyperText Transfer Protocol)
camada: [Camada de Aplicação](./Camada%20de%20Aplicação.md)

## Definição
É o protocolo da [Camada de Aplicação](./Camada%20de%20Aplicação.md) responsável pela transferência de hipermídia (texto, imagens, vídeos). É a base da World Wide Web.
- **Arquitetura:** [Cliente-Servidor](./Cliente-Servidor.md).
- **Estado:** É um protocolo **Stateless** (sem estado). O servidor não guarda informações sobre as requisições anteriores do cliente.
- **Gambiarra de Estado:** Para lembrar do usuário (login, carrinho), usa-se **[Cookies](./Cookies.md)**.

## Transporte
- **Protocolo:** Usa [TCP](./TCP.md).
- **Portas Padrão:** - `80` (HTTP - Texto Claro).
    - `443` (HTTPS - Criptografado com TLS).

## Tipos de Conexão (Evolução)
1. **Não Persistente (HTTP/1.0):** Abre e fecha uma conexão TCP para *cada* objeto. (Lento, alto overhead de Handshake).
2. **Persistente (HTTP/1.1):** Mantém a conexão TCP aberta para baixar múltiplos objetos sequencialmente.
    - *Problema:* Head-of-Line Blocking (um arquivo grande trava os pequenos atrás dele).
3. **Multiplexada (HTTP/2):** Usa uma única conexão TCP, mas divide os arquivos em *frames* e os envia misturados (intercalados) para evitar bloqueio.

## Mensagens
### Requisição (Request)
Formato: `MÉTODO URL VERSÃO`
- `GET`: Pede um objeto.
- `POST`: Envia dados (ex: formulários).
- Cabeçalhos importantes: `Host`, `User-Agent`, `Accept-Language`.

### Resposta (Response)
Formato: `VERSÃO CÓDIGO FRASE`
- `200 OK`: Sucesso.
- `301 Moved Permanently`: Redirecionamento.
- `304 Not Modified`: Objeto não mudou (usar Cache).
- `404 Not Found`: Arquivo não existe.
- `500 Internal Server Error`: Erro no código do servidor.

## Cybersec Insight
- **Sniffing:** HTTP puro trafega em texto claro. Senhas e cookies podem ser roubados com [Wireshark](./Wireshark.md).
- **Application Attacks:** Como é baseado em texto, é vulnerável a injeção de comandos se o servidor não sanitizar a entrada.
    - [SQL Injection](./SQL%20Injection.md): Inserir SQL no input.
    - [XSS](./XSS.md): Inserir scripts no input.
- **DoS:** Ataques como **Slowloris** abusam do HTTP Persistente para esgotar as conexões do servidor.
