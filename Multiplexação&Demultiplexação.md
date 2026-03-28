## Caminho do segmento

Um processo pode ter um ou mais [Socket](./Socket.md), portas as quais os dados passam da rede para o processo e do processo para a rede. A [Camada de Transporte](./Camada%20de%20Transporte.md) do hospedeiro destinatário entrega dados a um socket intermediário, não diretamente a um processo.

Podem haver diversos sockets no destinatário, cada um com sua identificação, podendo ser UDP ou TCP. Na extremidade receptora, a camada de transporte examina os campos do segmento que chegou e identifica a porta certa e direciona ao socket relativo.

A tarefa de entrega dos dados contidos em um segmento (pacote da camada de transporte) ao socket correto é denominado de *==**Demultiplexação***==.

Já a tarefa de reunir, no hospedeiro de origem, porções de dados provenientes de diferentes sockets, encapsular cada parte de dados com infos de cabeçalho (que posteriormente são usados na demultiplexação do destinatário) para criar segmentos, e passar esses segmentos para a camada de rede, é denominado finalmente de ***==Multiplexação==***.

*Obs: Esse contexto de Multiplexação / Demultiplexação não se aplica apenas a essa camada em específica, essa operação se aplica sempre que um único protocolo em uma camada for usado por vários protocolos na camada mais alta seguinte.*
