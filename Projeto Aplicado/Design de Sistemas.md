
#design #solução #diagram #requisitos 

## Roteiro

### 1. Entendendo o problema e definindo requisitos

	1. Qual o formato dos dados?
	2. Qual o padrão de banco de dados?
	3. Quais os requisitos mínimos (latência, síncrono ou assíncrono)?
	4. Quem são os usuários? Utilização fim (mobile app, web dev, web server). Quantos usuários (100, 100k, 100kk... )
	5. Quais features são necessárias?
	6. Requisitos não funcionais como segurança, consistência, taxas de atualização, corretude dos dados, **performance**, **escalabilidade**, disponibilidade (scalability, capacity, availability)
	7. Possíveis gargalos, estimativas de acesso e consumos de dados



### 2. Design de alto nível


	1. Comece por uma abordagem top-down
	2. Para soluções em API, através dos requisitos defina o input e output da request por endpoint, faça um esquemático:


**Request**: GET /v1/search
	Input parameters:
| Field     | Description             | Type   |
| --------- | ----------------------- | ------ |
| latitude  | lat of given location   | double |
| longitude | long of given location  | double |
| radius    | optional. default 500 m | int    |

Response:
```JSON
		
		{
			"total": 10,
			"businesses": [{ business object}]
		}
```

Uma vez definido o design das APIs, o próximo passo é definir um diagrama de alto nível da solução. Esse diagrama é um blue print geral da solução.:

![[Pasted image 20230213093842.png]]

Para um design de uma API comece pelo Load Balancer ou API Gateway. Não se aprofunde na tecnologia da persistência de dados (mysql, mongodb, cassandra, elasticsearch)

![[Pasted image 20230213094314.png]]
	
	
Enquanto estiver focado na solução de alto nível, deixe em aberto:
- Escalabilidade do banco de dados
- Concorrência
- Cenários de falha

Por último defina os modelos de dados (data model) e respectivos schemas. Neste ponto aborde também o padrão de acesso aos dados e frequência de escrita / leitura (read / write ratio)


### 3. Aprofunde a solução


Articule o problema.

Em cima do blue print de alto nível proponha solução (no mínimo duas) para cada ponto em aberto e discuta os trade-offs de cada solução. 

Por exemplo: a escolha do banco de dados interfere diretamente com a latência e usabilidade do sistema como um todo. No caso do google maps, um banco de dados apenas seria insuficiente para lidar com toda a demanda, então replica de bancos apenas para leitura ou mesmo bancos não relacionais passam a ser um melhor caminho.

Escolha uma solução e retorne para  os demais pontos em abertos



### 4. Amarre ao contexto (wrap up)


Sumarize o design, foque nos motivos de cada escolha