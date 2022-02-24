# DAW2: Centrality Closeness

***Language***

- [🇪🇸 Spanish](./README.md)
- ![united-kingdom](https://user-images.githubusercontent.com/55488676/152346624-aa99712d-5039-4382-af6e-90f71fe483c9.png)
 English
 
 <br />


Creation of a database based on graphs of UFC fighters in ```Neo4j```, imported from CSV files, and its subsequent analysis through the ```Centrality Closenness``` algorithm.


<img width="876" alt="2" src="https://user-images.githubusercontent.com/55488676/155516300-aa71331d-3735-4d7b-8797-6a4a469a2ab5.png">


<br />


## Requirements

To analyze the UFC fighter database through the Closeness of Centrality algorithm, a series of requirements must be met:

- Create a Database in Neo4j
- Install the ```APOC``` library in the Neo4j desktop application
- Install the ```Graph Data Science Library``` library in the Neo4j desktop application
- Add to the ```neo4j.conf``` file the line: ```apoc.import.file.enabled=true``` to be able to carry out the import of files
- Add the CSV documents to the Neo4j ```ìmport``` folder
- Import the database of UFC fighters and their relationships using CSV files


<br />


## Steps to follow for the creation of the UFC fighters database and analysis of the database with the Closeness of Centrality algorithm


#### Step 1: Create the database ####


The database and its relationships will be imported from the CSV files present in this same repository, using the [APOC](https://neo4j.com/labs/apoc/4.1/) library as follows:


```bash
CALL apoc.import.csv(
  [{fileName: 'file:/Fighters.csv', labels: ['FIGHTERS']}],
  [{fileName: 'file:/Fight_Against.csv', type: 'FIGHT_AGAINST'}],
  {delimiter: '|', arrayDelimiter: ',', stringIds: false}
)
```

<br />

#### Step 2: Analysis of the created database through the algorithm [Centrality Closeness](https://neo4j.com/docs/graph-data-science/current/algorithms/closeness-centrality/) ####

The database created in the previous step will be analyzed after importing it from the CSV files, using the centrality algorithm called ```Centrality Closeness``` to determine the score
of proximity centrality for each node of the graph.


<br />

To analyze the database with the algorithm mentioned above, the following query will be executed in the Neo4j browser:

```bash
CALL gds.alpha.closeness.stream({
  nodeProjection: 'FIGHTERS',
  relationshipProjection: 'FIGHT_AGAINST'
})
YIELD nodeId, centrality
RETURN gds.util.asNode(nodeId).name AS user, centrality
ORDER BY centrality DESC
```

After the execution of the previous query, the respective conclusions will be drawn from the results of the execution of the query itself, in order to analyze the information of the imported database.

<br />

## Job utilities

| Libraries                                                                               | Utilities                                           |
| --------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **[APOC](https://neo4j.com/labs/apoc/4.1/)**                                            | Library consisting of procedures and functions      |
| **[Graph Data Science Library](https://neo4j.com/docs/graph-data-science/current/)**    | Library with graphics algorithms for Neo4j          |
