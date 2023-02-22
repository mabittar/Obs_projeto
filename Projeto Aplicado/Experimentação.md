
Utilizar o REDIS e demais features como solução única

REDIS TIMESERIES
O Redis TimeSeries é um módulo Redis que adiciona uma estrutura de dados em série cronológica ao Redis. Ele permite inserções de alto volume junto com leituras de baixa latência. Os dados das séries cronológicas naturalmente têm o tempo como parâmetro principal de consulta. Com base nisto, podemos ter vários tipos de consultas agregadas. Uma forma adequada para armazenamento dos dados após leitura da fonte (CVM) e tratamento (transformação).

REDIS PUB/SUB
Em um Pub/Sub, a fonte do evento apenas "Publica" (publish) o evento para uma fila. Tal evento é temporário. Ele se perde imediatamente após a sua criação - a menos que seja captado por um "Assinante" (subscriber). Poderíamos ter vários assinantes esperando por eventos de qualquer "publisher". Tal comunicação é útil quando o momento do evento em si é tão importante quanto os dados que ele carrega.

Observe aqui que o assinante não se importa com quem publicou o evento e a editora não se importa com quem assina o evento. Ambos trabalham independentemente, levando a um desacoplamento perfeito. Entretanto, se por algum motivo, não houver assinante ativo quando o evento for publicado, esse evento será perdido e não poderá ser recuperado.

A sintaxe do Pub/sub é muito simples. Podemos assinar um canal usando o comando SUBSCRIBE e depois publicar para esse canal usando o PUBLICIDADE. 

REDIS STREAM
O stream por outro lado, é mais permanente. A "fonte do evento" acrescenta continuamente os eventos a um "fluxo de eventos". Outro serviço que está interessado nestes eventos pode "ouvir" este fluxo e "consumir" os eventos no fluxo. Os eventos no fluxo são "persistidos" por um tempo configurado no sistema. Isto proporciona um sistema robusto onde os ouvintes podem consumir os eventos em seu próprio ritmo.

O streaming é melhor que o pub/sub? Não é necessário! O Streaming é mais robusto, com certeza. No entanto, implica em uma sobrecarga que pode não ser necessária. O Pub/Sub é leve e mais apto para a exigência às vezes. Qualquer um dos padrões tem seu próprio valor, e é tarefa do arquiteto identificar e implementar o padrão apropriado no caso de uso em questão.