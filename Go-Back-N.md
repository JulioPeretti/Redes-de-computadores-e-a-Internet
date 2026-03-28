# Go Back N (GBN)
## Definição
No protocolo GBN, um remetente é autorizado a transmitir múltiplos pacotes sem esperar reconhecimento, mas fica limitado a ter não mais do que algum número máximo permitido, N, de pacotes não reconhecidos na 'Tubulação'.

A faixa de números permitidos para pacotes transmitidos, porém ainda não reconhecidos, pode ser vista como uma janela de tamanho N. À medida que o protocolo opera, a janela se desloca para frente sobre o espaço de números da sequencia. Por essa razão, N é muitas vezes denominado de ==tamanho de janela==, e o protocolo GBN em si, protocolo de ==janela deslizante==.

O destinatário apenas armazena uma variavel referente ao próximo numero esperado da sequencia, se ele receber algo fora de ordem, ele descarta o pacote e aguarda o reenvio do remetente.

#### Base:
Número de sequencia do mais antigo pacote não reconhecido.
#### NextseqNum:
O número do próximo pacote que vamos criar.

Os algoritmos de Go Back N possuem variáveis que permitem a janelas e locomover para frente em tempo real, mais parecendo com a programação propriamente dita.

#### A janela esta cheia?
NextseqNum < base + N

#### Existem pacotes viajando ou esperando ACK?
base < NextseqNum

#### Tudo que foi enviado já chegou?
base == NextseqNum

#### Timer:
Ao enviar o primeiro pacote da janela (base == NextseqNum), o timer é ligado, se ele estourar, tudo que vem depois da base, é reenviado.


## Esquema de envio/recebimento 

### "GBN Aperfeiçoado":
- [Repetição Seletiva (SR)](./Repetição%20Seletiva%20(SR).md)
