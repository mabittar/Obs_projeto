
O Design Pattern de Mensageria é um padrão de projeto de software que define uma abordagem para comunicação entre componentes de software distribuídos. Ele se concentra em soluções para problemas comuns enfrentados na criação de aplicativos distribuídos, como integração de sistemas, escalabilidade, alta disponibilidade e tolerância a falhas.

O Design Pattern de Mensageria envolve o uso de mensagens para a comunicação entre componentes, em vez de invocar diretamente outros componentes. Cada componente pode ser pensado como um "produtor" ou "consumidor" de mensagens. O produtor envia mensagens para o sistema, enquanto o consumidor as recebe e as processa.

Os Design Patterns de Mensageria incluem vários padrões, como o padrão Publish/Subscribe, o padrão Request/Reply e o padrão Message Queue. Cada padrão define uma abordagem específica para a comunicação de mensagens entre componentes distribuídos.

Ao utilizar o Design Pattern de Mensageria, é possível criar soluções de software distribuídas que são escaláveis, flexíveis, tolerantes a falhas e de fácil manutenção. Além disso, ele ajuda a garantir que o software seja integrado de maneira eficiente, sem prejudicar o desempenho ou a disponibilidade do sistema.

## Pub/Sub
O padrão Publish/Subscribe (também conhecido como "Pub/Sub") é um modelo de comunicação em que os componentes de software se registram como interessados ou assinantes em receber mensagens de determinados tipos. Quando uma mensagem é publicada, ela é entregue a todos os componentes registrados como assinantes nesse tipo de mensagem.

O produtor dessa mensagem é um outro componente isolado, que pode ou não se importar com o resultado final

No padrão Pub/Sub, existe um intermediário (ou "broker") que gerencia a publicação e a entrega das mensagens. Este intermediário é responsável por armazenar mensagens enviadas por produtores e entregá-las aos consumidores correspondentes.

## Message Queue

O padrão Message Queue (fila de mensagens) é um modelo de comunicação em que as mensagens são armazenadas em uma fila antes de serem processadas pelos consumidores. Neste padrão, o intermediário (ou "broker") é responsável por garantir que as mensagens sejam entregues em ordem, evitando que mensagens sejam perdidas ou processadas duplicadamente.

A principal diferença entre os dois padrões é que, no padrão Pub/Sub, as mensagens são entregues a todos os componentes interessados, enquanto no padrão Message Queue, as mensagens são entregues a um único componente, na ordem em que foram adicionadas na fila.

Ambos os padrões são amplamente utilizados em aplicativos distribuídos, especialmente em sistemas que precisam lidar com grandes volumes de mensagens ou processamento em lote. Eles ajudam a garantir a escalabilidade, a alta disponibilidade e a tolerância a falhas de sistemas distribuídos.

### Detalhes Técnicos

https://zguide.zeromq.org/docs/chapter2/#Messaging-Patterns

Os workers conectam-se a montante ao publisher, e a jusante ao funil. Isto significa que você pode adicionar workers arbitrariamente. Se os workers se conectarem a seus pontos finais, você precisará (a) mais pontos finais e (b) modificar o publisher e/ou o funil cada vez que você adicionar um worker. Dizemos que o publisher e o funil são partes estáveis de nossa arquitetura e os workers são partes dinâmicas da mesma.


Os padrões de mensageria são implementados por pares de soquetes com tipos correspondentes. Em outras palavras, para entender os padrões é necessário entender os tipos de soquetes e como eles funcionam em conjunto. Na maioria das vezes, isto só requer estudo; 

**Request-reply**: Resposta à solicitação, que conecta um conjunto de clientes a um conjunto de serviços. Este é um padrão de chamada de procedimento remoto e distribuição de tarefas.

**Pub-sub**: que conecta um conjunto de editores a um conjunto de assinantes. Este é um padrão de distribuição de dados.

**Pipeline**: que conecta os nós em um padrão de fan-out/fan-in que pode ter vários passos e loops. Este é um padrão paralelo de distribuição de tarefas e coleta de dados.

**Exclusive pair**: par exclusivo, que conecta dois soquetes exclusivamente. Este é um padrão para conectar dois fios em um processo, não confundir com pares "normais" de soquetes.


### Etapas de um sistema de mensageria

1. Conectar o publisher a uma fila / tópico
2. Criar a mensagem
3. Enviar para a fila / tópico
4. Conectar o assinante a uma fila / tópico
5. Receber a mensagem
6. Acessar o conteúdo da mensagem
7. Processar o conteúdo


#design_patterns #mensageria #pubsub
