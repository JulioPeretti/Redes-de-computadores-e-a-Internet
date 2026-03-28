# Camada de Transporte
modelo: [Camadas de TCP IP](./Camadas%20de%20TCP%20IP.md)

## Definição
Posicionada entre a camada de aplicação e a de Redes, fornece serviços de comunicação diretamente aos processos de aplicação que rodam em hospedeiros diferentes.

## Características
- Antes de falar sobre UDP e TCP, é importante ressaltar que a camada de Rede, situada abaixo da de Transporte, possui um protocolo denominado IP (Internet Protocol), o qual realiza esforço de entrega mas não garante a entrega dos segmentos. Cada hospedeiro possui um endereço IP, porém isso é aprofundado em [Camada de Rede](./Camada%20de%20Rede.md).

- Ampliam os serviços de entrega IP entre dois sistemas finais para um serviço de entrega entre dois processos que rodam nos sistemas finais. Essa ampliação de entrega hospedeiro hospedeiro para entrega processo a processo é denominada de [Multiplexação&Demultiplexação](./Multiplexação&Demultiplexação.md) da camada de transporte.

- Cada Socket respectivo possui sua porta com identificador exclusivo e cada segmentos por sua vez possuem campos especiais que indicam a qual porta devem ser entregues. Os números de porta da faixa de 0 a 1023 são denominados bem conhecidos, eles são restritos e reservados para protocolos famosos; Ex: HTTP 80, FTP 21.

## [Transferência confiável de dados](./Transferência%20confiável%20de%20dados.md)
Engloba outras camadas como a [Camada de Aplicação](./Camada%20de%20Aplicação.md) e a [Camada de Enlace](./Camada%20de%20Enlace.md).
É o problema mais importante de trabalho em Rede.


## Principais Protocolos


### UDP
- [UDP](./UDP.md) - Transporte não orientado a conexão.

### TCP 
- [TCP](./TCP.md) - Transporte orientado a conexão.
