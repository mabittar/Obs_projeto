## DESAFIO

## INTRODUÇÃO
Como o mundo está se enraizando na nova era de serviços em nuvem, um desafio fundamental que assombra todos os arquitetos é identificar a solução tecnológica correta para o sistema. O grande número de alternativas e suas combinações é suficiente para deixar qualquer profissional com dúvidas.

Os desafios de hoje não se limitam à identificação de uma boa tecnologia ou ferramenta para a tarefa. Não estamos escolhendo entre uma boa ferramenta e uma má. A escolha é identificar um conjunto apropriado dentro de uma vasta opção de ferramentas e tecnologias disponíveis. Precisamos encontrar o subconjunto certo de tecnologias, que possam se complementar e funcionar bem em conjunto.

A arquitetura pretende ser facilitadora no processo de desenvolvimento de sistemas web, visando agilizar não somente o atendimento ao público, mas também gerando poucos erros em produção a cada ciclo de release.

#### Por que a Arquitetura de software é importante.

 A arquitetura de software é importante, pois ajuda a garantir que o software seja de alta qualidade, fácil de manter, escalável, flexível e de desempenho otimizado, o que é crítico para o sucesso de projetos de software a longo prazo. Podemos observar em detalhes cada ponto abordado:

1.  Qualidade do software: Uma boa arquitetura de software ajuda a garantir que a aplicação seja de alta qualidade, mantendo-o escalável, flexível, confiável e fácil de manter.
2.  Facilidade de manutenção: Uma arquitetura clara e bem projetada torna o software mais fácil de manter e corrigir, pois os componentes são organizados de maneira lógica e fácil de entender.
3.  Flexibilidade: Uma boa arquitetura de software deve ser projetada para permitir mudanças no futuro, sem prejudicar o funcionamento do software. Isso permite que o software seja adaptado às mudanças no ambiente de negócios.
4.  Melhor desempenho: Uma arquitetura de software bem projetada pode ajudar a garantir que o software tenha desempenho otimizado, gerenciando de maneira eficiente recursos como memória, processamento e largura de banda de rede.
5.  Melhor tomada de decisão: A arquitetura de software é um importante ponto de partida para tomar decisões de design, implantação e melhoria de software, pois permite visualizar e avaliar a estrutura geral do software.

Ou seja, a arquitetura de software é inerente ao processo de desenvolvimento de software. Uma boa arquitetura irá sustentar sistemas e soluções ao longo da vida do projeto, desde a concepção, passando pelo desenvolvimento e monitoramento, até o seu descomissionamento.

![[Cloud Architecture]]

![[CANVAS.canvas]]
### MATRIZ CSD


![[Matriz CSD]]

### MATRIZ POEMS


![[POEMS.canvas]]



## PROPOSTA
O desafio de extração de dados do mercado financeiro para consumo em uma aplicação envolve a coleta, processamento e armazenamento de dados de mercado em tempo real para serem utilizadas por vários usuários em uma plataforma em diversas aplicações e soluções. Alguns dos requisitos desta aplicação incluem:

1.  Alto desempenho: é necessário garantir que a aplicação possa lidar com uma grande quantidade de dados financeiros e fornecer informações atualizadas rapidamente para os usuários.
2.  Segurança dos dados: é crucial proteger os dados financeiros contra acesso não autorizado e garantir a privacidade dos usuários.
3.  Múltiplos usuários: a aplicação deve ser projetada para lidar com vários usuários acessando grande massa de dados financeiros ao mesmo tempo.

### SOLUÇÃO

Boas práticas de arquitetura de software visam contribuir para o atendimento dos objetivos, respeitando restrições, atingindo atributos de qualidade.

#### Dividir para Conquistar:
Como já explanado anteriormente, um dos pontos fundamentais da arquitetura da nossa solução será o alto desempenho, flexibilidade e escalabilidade.

Utilizando a estratégia "Divide and Conquer" é possível abordar o problema  e dividir sua complexidade em subproblemas menores de fácil entendimento e, assim, endereçar soluções de forma eficiente, definindo blocos de responsabilidades, tornando a software mais fácil de entender, aprender, fazer  futuras expansões e manutenções.

A aplicação deste padrão envolve três etapas principais:

1.  Análise do problema: O primeiro passo é identificar o problema complexo que precisa ser resolvido e analisá-lo para identificar subproblemas menores e independentes.
2.  Solução de subproblemas: Em seguida, cada subproblema é solucionado individualmente. Esta etapa pode envolver a aplicação de técnicas de resolução de problemas semelhantes ou o uso de algoritmos específicos para solucionar cada subproblema.
3.  Combinação de soluções: Por fim, as soluções para cada subproblema são combinadas para obter a solução final para o problema original.

Ao olhar para essa estratégia, um dos design patterns já salta aos olhos que é o de mensageria:

#### Design Pattern

![[Mensageria]]

#### Padrão arquitetural
Aliado ao padrão de mensageria podemos pensar no modelo de arquitetura em Micro serviços ( #microservices) 


![[Microservices]]

### Arquitetura inicial Proposta

![[arch.jpg]]


![[Diagrama da aplicação]]



Em um ambiente financeiro, confiabilidade, segurança e desempenho devem andar de mãos dadas. O Redis Cache é  um componente padrão e largamente utilizado em soluções na web para qualquer empreendimento significativo. Para tornar a vida do arquiteto mais simples, aliado a essa solução de alto desempenho a Redis INC criou um pacote completo de ferramentas que fornecem todos os principais componentes de uma arquitetura Microservice - o Redis Stream, Redis Pub Sub, Redis Search, Redis AI, Redis JSON, Redis Graph, Redis Time series, e muitas outras.

A stack Redis (Redis JSON, Redis Search, Redis Timeseries, Redis Graph, e Redis Bloom) reduz significativamente o caos tecnológico. Juntamente com estes, as estruturas de dados Pub-Sub e Streaming permitem uma comunicação assíncrona elegante entre seus micro serviços.

A solução proposta é um modelo arquitetural em micro serviços, divido em uma API Rest, com  possui endpoints específicos e concentrando as regras de negócio.

- listar endpoints

 regras de negócio
 - ao realizar uma request a API verifica e valida se todos os campos necessários foram passados e se os campos estão no formato esperado;
 - após a validação da request verifica se o CNPJ já existe na base de dados:
	 - caso exista: vai verificar o último dia que houve atualização e confrontar com a data do servidor onde a aplicação esta rodando, caso os dados já sejam atuais irá apenas devolver os resultados a partir do banco de dados;
	 - a aplicação irá executar uma consulta no site da CVM, caso o CNPJ não seja encontrado será devolvido um erro pro usuário de CNPJ não encontrado.
	 - caso não exista na base de dados local ou necessite de atualização irá iniciar o fluxo de atualização. Cada mês necessário de atualização é publicado como uma mensagem independente para a fila do Pub/Sub.
- Uma outra aplicação (queue ou fila) é responsável por realiza a carga dos dados a partir do site da CVM, sendo essa aplicação uma assinante do fluxo de mensageria. 
- para cada mensagem na fila a aplicação irá disponibilizar um thread (processador) livre que será responsável por fazer a chamada no site da CVM, realizando a carga dos dados, o processamento e ordenação dos dados obtidos para aquela mensagem (referente a um mês do fundo).  Após a ordenação a aplicação ainda é responsável por executar a persistência desses dados em forma de TimeSeries
- caso necessário a aplicação foi arquitetada para trabalhar de forma isolada, sendo possível escalonar horizontalmente esse etapa, criando um pool de assinantes, acelerando o processo consumo e processamento das mensagens na fila.


![[Pasted image 20230208190658.png]]