# Determining the most important node of a graph depends on your definition of importance. This definition itself depends on the goal you are trying to achieve

## Pesquisa de quantas demandas foram feitas por Pessoa
MATCH (n:PESSOA)-[r:REALIZAR]->()
RETURN n.nome, count(r) as outgoingDegree
ORDER BY outgoingDegree DESC

## Pesquisa de quantas demandas foram feitas para determinado processo
MATCH (p:PROCESSO)<-[r:ATENDER]-()
RETURN p.numero, count(r) as ingoingDegree
ORDER BY ingoingDegree DESC

MATCH (p:PROCESSO)
OPTIONAL MATCH (p)<-[r:ATENDER]-()
RETURN p.numero as numeroProcesso, count(r) as incomingDegree
ORDER BY incomingDegree DESC

