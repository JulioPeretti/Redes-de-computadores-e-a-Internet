## Definição:
Vem para solucionar a demora do **pare e espere**, adotando envio sequencial de pacotes , uns atrás dos outros, sem esperara por reconhecimentos, essa técnica é conhecida como pipelining e é a solução utilizada hoje em dia para envio seguro.

O **pare e espere** peca no quesito que apenas uma minúscula porção do tempo você gasta realmente transmitindo algo ao enlace, a maioria do tempo é gasto esperando resposta. O que resulta no cabo de fibra ótica estando inutilizado 99%+ do tempo.

O pipelining resolve isso adicionando:
1. Faixa ampliada de números de sequencia:
	   Cada pacote precisa ter um número exclusivo.
2. Remetente e destinatário precisam reservar buffers.
	   O remetente tem que no mínimo ter um buffer para os pacotes transmitidos que ainda não foram reconhecidos pelo destinatário e até um para pacotes recebidos sem erro.


## Recuperação de erros em pipelining
- [Go-Back-N](./Go-Back-N.md)
