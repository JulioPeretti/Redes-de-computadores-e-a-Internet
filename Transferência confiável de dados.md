# Definição 
Busca levar dados por um canal sem que os dados sejam corrompidos,( trocado de 0 para 1 ou vice-versa) nem perdido, e todos devem ser entregues na mesma ordem que enviados. Isso descreve exatamente o TCP. É um desafio devido ao protocolo ser executado sob um protocolo não confiável, como o IP.

## RESUMO:

# Aprofundamento:
### rdt 1.0 (reliable data transfer)
Se trata da transferência perfeita, em que o canal subjacente é totalmente confiável, as maquinas de estado mudam apenas para o próprio estado delas (esperar a chamada da camada de cima e esperar a chamada de baixo), as alterações apenas consistem em mandar o pacote e receber o pacote, sem maiores confusões.

### rdt 2.0
Possui um grave problema de não tratar possíveis erros nos pacotes ACK e NAK, incapacitando o remetente de confirmar o recebimento ou não.
É um modelo mais realista de canal subjacente em que os bits estão sujeitos a serem corrompidos. 
Esses erros de bits ocorrem em geral nos componentes físicos enquanto o pacote é transmitido, propagado e armazenado.

## Protocolos ARQ (Automatic Repeat reQuest)
São protocolos de transferência de dados que funcionam baseados na resposta constante por parte do remetente informando o recebimento dos dados.
São exigidas 3 capacitantes adicionais dos protocolos ARQ para manipular os erros de bits:
1. Detecção de erros
	   Necessita-se um mecanismo, como o visto na soma de verificação **UDP**, para averiguar quando erros ocorrerem. Essas técnicas de verificação exigem que bits extras sejam enviados do remetente ao destinatário com a finalidade de serem usados na soma de verificação do **protocolo rdt 2.0.**
2. Realimentação do destinatário
	   Com a intenção de informar o remetente sobre o recebimento ou não dos pacotes, o destinatário realimenta o remetente com pacotes ==**ACK (*Acknowledgemente*)**== ou ==**NACK (*negative acknowledgement*)**.== Pacotes esses que a princípio apenas precisam conter apenas 1 bit indicando o recebimento ou não. 
3. Retransmissão
	   Um pacote recebido com erro no destinatário deve ser retransmitido pelo remetente.

O lado remetente espera chamada de cima para enviar pacotes, após receber a chamada, cria os pacotes e os envia junto com os bits da soma de verificação e muda seu estado para esperar um **ACK** ou **NAK.** Caso receba um **NAK**, ele reenvia o mesmo pacote e espera novamente um **ACK** ou **NAK**. É apenas quando receber um **ACK** que ele retorna ao estado de espera da chamada de cima, para proceder o envio de novos pacotes. 

O lado destinatário espera sempre pela chamada de baixo, ele verifica se o pacote recebido esta corrompido, se estiver responde um **NAK**, se não estiver, ele extrai o pacote e repassa para a camada superior o pacote recebido, e devolve um **ACK** para confirmar o recebimento íntegro.

### rdt 2.1
O rdt 2.1 corrige o problema de erro no ACK ou NAK com um envio de numero 0 ou 1 para cada pacote enviado. Funciona da seguinte forma: O remetente envia o pacote 0, o receptor recebe e envia o ACK, o ACK pode ser corrompido e virar lixo, então o remetente recebe algo corrompido e na duvida reenvia o pacote 0, o destinatário novamente recebe o pacote 0, percebe que já o possui e o descarta enviando novamente o ACK para o remetente.

### rdt 2.2
Muito parecido com o 2.1 esse modelo retira o pacote NAK, o substituindo por ACK 0 ou ACK 1.
Funcionamento: O remetente envia o pacote 1, o destinatário pode receber o pacote 1 corrompido, nesse caso o destinatário devolve um pacote ACK 0, que demonstra que o ultimo bem recebido foi o ACK 0, o remetente percebe o ACK 0 duplicado e reenvia o pacote 1.

### rdt 3.0
É conhecido como protocolo pare e espere.
Agora ataca o problema de perda de pacote, não sua corrupção, a solução simplificada é esperar um determinado tempo ponderado para reenviar o pacote, se por acaso o destinatario receber 2 pacotes devido ao reenvio do remetente, não é um problema uma vez que o rdt 2.2 já soluciona pacotes duplicados. A alteração do rdt 3.0 recai sobre o remetente apenas, que deve introduzir um temporizador para todas as vezes que um pacote for enviado. 
Ele é absurdamente lento em redes de longa distancia devido a demora do timer. (Alto RTT).
Funcionamento: O remetente manda um pacote e liga um cronometro, se o ACK chegar antes do cronometro estourar, tudo certo, caso o cronometro estoure, o remetente reenvia o pacote


# Próximos passos 
Devido a lentidão em longas distancias do protocolo 3.0 **pare e espere**, temos [Transferência confiável com pipelining](./Transferência%20confiável%20com%20pipelining.md).



*Obs: Este estudo recai em maquinas de estado finito, aprofundar mais pode ser interessante.*
