# Cypher Projections
https://neo4j.com/docs/graph-data-science/current/graph-create/


// It enables us to create relationships on the fly that will only be created in the projected graph and not in the Neo4j graph
CALL gds.graph.create.cypher(
    graphName::STRING,
    nodeQuery::STRING,
    relationshipQuery::STRING,
    configuration::MAP
)

// Exemplo
// Cypher projections are really useful to add relationships or properties on the fly in the projected graph.
CALL gds.graph.create.cypher(
    "myProjectedCypherGraph",
    "MATCH (u:User) RETURN id(u) as id",
    "MATCH (u:User)-[:FOLLOWS]->(v:User) RETURN id(u) as source, id(v) as destination"
)


#Listar os gráficos existentes
CALL gds.graph.list()
YIELD graphName, nodeCount, relationshipCount
RETURN graphName, nodeCount, relationshipCount
ORDER BY graphName ASC

#Apagar um grafo por nome
CALL gds.graph.drop('NOME_GRAFO') YIELD graphName;


