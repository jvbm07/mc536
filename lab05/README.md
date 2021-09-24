# Modelo para Apresentação do Lab05 - Marcadores e Taxonomia em Cypher

Estrutura de pastas:

~~~
├── README.md  <- arquivo apresentando a tarefa
~~~

# Aluno
* `237833`: `João Vitor Baptista Moreira`

## Tarefa de Cypher sobre Marcadores e Taxonomia

## Tarefa 1

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, sem considerar as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador ) - [:Pertence]-> (c:Categoria) 
WHERE c.id = "Serviços" 
RETURN m,c
~~~

## Tarefa 2

Escreva em Cypher uma consulta que retorne os marcadores da categoria `Serviços`, considerando as categorias subordinadas.

### Resolução
~~~cypher
MATCH (m:Marcador) - [:Pertence]-> (c:Categoria)
MATCH (filho:Categoria) - [:Superior]-> (serv:Categoria {id:"Serviços"})
MATCH (neto:Categoria) - [:Superior]-> (aux:Categoria)
WHERE (c.id = serv.id or c.id = neto.id or c.id = aux.id) and (aux.id = filho.id or aux.id = serv.id)

RETURN m

~~~
