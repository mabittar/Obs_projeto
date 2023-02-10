*Micro serviços são serviços com interfaces públicas enxutas e extremamente coesas.*

A interface pública de um serviço habilita a “entrada e saída” de informações, tanto de forma síncrona – em um modelo baseado em _request/response_ – quanto assíncrona – através de troca de mensagens com comandos ou eventos.
Interfaces pública enxutas e coesas, bem delimitadas, fazem com que micro serviços sejam mais fáceis de entender, tanto em sua lógica interna quanto em demandas de integração/cooperação.

---
Atenção:
"O trade-off negativo da reutilização é o #acoplamento. Quando um arquiteto projeta um sistema favorecendo o reuso, ele também favorece ao acoplamento para permitir esse reuso, seja por herança ou composição."
**Neil Ford**
----
#### Oito falácias da computação distribuída
Em 1994, Peter Deutsch, que trabalhou na Sun Microsystems, consolidou uma lista de 7 falácias frequentemente associadas a sistemas distribuídos. Mais tarde, em 1997, James Gosling adicionou um item a essa lista, criando a comumente conhecida relação das oito falácias da computação distribuída. São elas:

-   A rede é confiável
-   A latência é zero
-   A largura de banda é infinita
-   A rede é segura
-   A topologia da rede nunca muda
-   Existe um administrador
-   Custo de transferência de dados é zero
-   A rede é homogênea


## O Padrão de Projetos - Micro Serviços
O padrão de projeto Microservices é um modelo de arquitetura de software que permite a criação de aplicativos complexos como uma coleção de pequenos serviços independentes e altamente especializados. Cada serviço é projetado para realizar uma tarefa específica e é responsável por sua própria funcionalidade, dados e escalabilidade.

Este padrão se baseia na ideia de que grandes aplicativos monolíticos são difíceis de manter e escalar, e que é mais fácil trabalhar com aplicativos menores e mais focados. Ao utilizar o padrão Microservices, é possível criar aplicativos altamente escaláveis, resilientes e flexíveis, que são mais fáceis de manter e atualizar.

As empresas estão percebendo cada vez mais a economia de custo ao se
resolver problemas de implantação e melhorar as operações de produção e de DevOps
usando os containers. Essa soluções usando containers auxiliam as empresas a
criar e implantar aplicativos com a velocidade e a escala da nuvem, seja qual for a
escolha de plataformas ou de ferramentas.

O Docker está se tornando o verdadeiro padrão no setor de containers, com
suporte dos fornecedores mais significativos nos ecossistemas do Windows e do Linux. No
futuro, o Docker provavelmente estará onipresente em qualquer datacenter na nuvem
ou no local.As empresas estão percebendo cada vez mais a economia de custo ao se
resolver problemas de implantação e melhorar as operações de produção e de DevOps
usando os containers.

A aplicação deste padrão envolve três etapas principais:

1.  Identificação de serviços: O primeiro passo é identificar as funcionalidades do aplicativo e dividi-las em serviços independentes e altamente especializados.
2.  Desenvolvimento de serviços: Em seguida, cada serviço é desenvolvido de forma independente, utilizando tecnologias e ferramentas apropriadas.
3.  Integração de serviços: Por fim, os serviços são integrados para formar o aplicativo final. Esta integração pode ser realizada através de mensagens, APIs ou outras técnicas de comunicação.


#architecture #microservices #docker