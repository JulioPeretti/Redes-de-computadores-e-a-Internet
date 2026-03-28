# UDP (User Datagram Protocol)
camada: [Camada de Transporte](./Camada%20de%20Transporte.md)

## Definição
É um protocolo da camada de transporte não orientado a conexão, ou seja, não possui Handshake, não possui apresentação. É quase como se a aplicação estivesse interagindo direto com o IP da camada de rede. 

## Funcionalidade
Em suma, o **UDP** pega as mensagens da aplicação, anexa número de porta de origem e destino, adiciona outros dois pequenos campos e já o passa adiante para a [Camada de Rede](./Camada%20de%20Rede.md), que encapsula o **segmento** em um **Datagrama IP** e faz seu melhor para entregar ao receptor. Se tudo ocorrer corretamente e o segmento chegar ao hospedeiro receptor, o UDP usará o número da porta [Socket](./Socket.md) de destino para entregar os dados do processo de aplicação correto. Um exemplo de uso do UDP é nas requisições [DNS](./DNS.md).

## Peculiaridades:
- Melhor controle no nível da aplicação:
	  Possui maior controle de quais dados são enviados e quando. Ao contrário do TCP, o UDP não possui controle de envio ou gargalo, uma vez que não existe ordem de prioridade. Sendo mais útil para aplicações de tempo real.

- Não há estabelecimento de conexão:
	  Devido a ausência de Handshake, ele se torna mais ágil, já que não espera resposta alguma, tornando-se ideal para o DNS.

- Não há estados de conexão:
	  Não possui buffers de envio ou recebimento nem controle de congestionamento, a ausência de tantas funcionalidades o torna leve para aplicações que possuem grande número de conexões simultâneas. 

- Pequeno cabeçalho de pacote:
	  TCP - 20 bytes
	  UDP - 8 bytes


## Soma de verificação:
Serve para identificar erros, é usada para determinar se bits dentro do segmento foram alterados durante sua movimentação da origem ao destino. O UDP do remetente realiza **complemento de 1** da soma de todas as palavras de 16 bits, levando em conta o "**vai um**".  Realiza as somas e inverte todos os números binários, esse resultado é a verificação. Ele realiza esse processo pois não é garantia que todas as camadas de enlace realizem esse processo sozinhas.

Mesmo tendo esse monitoramento de erros, ele nada faz sobre alem de ou descartar o pacote, ou envia-lo a aplicação com um aviso.
