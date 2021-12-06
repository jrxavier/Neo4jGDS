# Path Finding
Importante! O algorithm considera a direção das relações bem como um pesso associado
Para eliminar a direção, na criação do grafo precisamos definir a orientação como "UNDIRECTED"
Exemplo aplicado ao Grafo de Demandas GIIN:

CALL gds.graph.create("grafo", "*", {
           ROAD: {
               type: '*',
               orientation: 'UNDIRECTED',
               properties: "custo"
         }
     }
)

# Uso do algoritmo para pesquisar o caminho entre duas pessoas
MATCH (source:PESSOA {email: 'AryD@cvm.gov.br'}), (target:PESSOA {email: 'ana.gabriela@cvm.gov.br'})
CALL gds.shortestPath.dijkstra.stream('grafo', {
    sourceNode: source,
    targetNode: target,
    relationshipWeightProperty: 'custo'
})
YIELD index, sourceNode, targetNode, totalCost, nodeIds, costs, path
RETURN
    index,
    gds.util.asNode(sourceNode).name AS sourceNodeName,
    gds.util.asNode(targetNode).name AS targetNodeName,
    totalCost,
    [nodeId IN nodeIds | gds.util.asNode(nodeId).name] AS nodeNames,
    costs,
    nodes(path) as path
ORDER BY index
