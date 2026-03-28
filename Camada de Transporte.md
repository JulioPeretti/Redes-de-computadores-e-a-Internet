# Camada de Transporte

## Definição
Posicionada entre a camada de aplicação e a de Redes, fornece serviços de comunicação diretamente aos processos de aplicação que rodam em hospedeiros diferentes.

## Características
- **IP (Internet Protocol):** A camada de Rede abaixo realiza esforço de entrega, mas não garante a chegada dos segmentos. Detalhes em [Camada de Rede](./Camada%20de%20Rede.md).
- **Multiplexação & Demultiplexação:** Amplia a entrega hospedeiro-hospedeiro para entrega processo-a-processo.
- **Portas:** Cada Socket possui uma porta exclusiva. Faixa 0-1023 (Well-known): HTTP 80, FTP 21.

## Transferência Confiável de Dados
Engloba outras camadas como a de Aplicação e Enlace. É considerado o problema mais importante de trabalho em Rede.

## Principais Protocolos
### UDP
- Transporte não orientado a conexão.

### TCP 
- Transporte orientado a conexão.
