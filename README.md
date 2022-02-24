## DAW2: Centrality Closeness


<br />

***Idioma***
- 🇪🇸 Español
- [![united-kingdom](https://user-images.githubusercontent.com/55488676/152346624-aa99712d-5039-4382-af6e-90f71fe483c9.png) Inglés](https://github.com/Danilooo99/Prompt-Style/blob/master/README.md)


<br />


Creación de una base de datos basada en grafos de luchadores de la UFC en ```Neo4j```, importada desde ficheros CSV, y su posterior análisis a través del algoritmo ```Centrality Closenness```.


<img width="876" alt="2" src="https://user-images.githubusercontent.com/55488676/155516300-aa71331d-3735-4d7b-8797-6a4a469a2ab5.png">


<br />


## Requisitos

Para analizar la base de datos de luchadores de la UFC a través del algoritmo de Cercanía de centralidad hay que cumplir una serie de requisitos:

- Crear una Base de datos en Neo4j
- Instalar la librería ```APOC``` en la aplicación de escritorio de Neo4j
- Instalar la librería ```Graph Data Science Library``` en la aplicación de escritorio de Neo4j
- Añadir al fichero ```neo4j.conf``` la línea: ```apoc.import.file.enabled=true``` para poder llevar a cabo la importación de ficheros
- Añadir los documentos CSV a la carpeta ```ìmport``` de Neo4j
- Importar la base de datos de luchadores de la UFC y sus relaciones haciendo uso de los ficheros CSV


<br />


## Pasos a seguir para la creación de la base de datos de luchadores de la UFC y análisis de la base de datos con el algoritmo de Cercanía de centralidad


#### Paso 1: Creación de la base de datos ####


La base de datos y sus relaciones serán importadas desde los ficheros CSV presentes en este mismo repositorio, haciendo uso de la librería [APOC](https://neo4j.com/labs/apoc/4.1/) de la siguiente manera:


```bash
CALL apoc.import.csv(
  [{fileName: 'file:/Fighters.csv', labels: ['FIGHTERS']}],
  [{fileName: 'file:/Fight_Against.csv', type: 'FIGHT_AGAINST'}],
  {delimiter: '|', arrayDelimiter: ',', stringIds: false}
)
```

<br />

#### Paso 2: Análisis de la base de datos creada a través del algoritmo [Centrality Closeness](https://neo4j.com/docs/graph-data-science/current/algorithms/closeness-centrality/) ####

Se analizará la base datos creada en el paso anterior tras la importación de la misma desde los ficheros CSV, haciendo uso del algoritmo de centralidad denominado ```Centrality Closeness``` para determinar la puntuación
de centralidad de proximidad para cada nodo del grafo.

<br />

Para analizar la base de datos con el algoritmo mencionado anteriormente se ejecutará en el navegador de Neo4j la siguiente consulta:

```bash
CALL gds.alpha.closeness.stream({
  nodeProjection: 'FIGHTERS',
  relationshipProjection: 'FIGHT_AGAINST'
})
YIELD nodeId, centrality
RETURN gds.util.asNode(nodeId).name AS user, centrality
ORDER BY centrality DESC
```

Tras la ejecución de la consulta anterior, se sacarán las conclusiones respectivas de los resultados de la ejecución de la propia consulta, para así, analizar la información de la base de datos importada.


<br />

## Utilidades del trabajo

| Librerías                                                                               | Utilidad                                            |
| --------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **[APOC](https://neo4j.com/labs/apoc/4.1/)**                                            | Biblioteca que consta de procedimientos y funciones |
| **[Graph Data Science Library](https://neo4j.com/docs/graph-data-science/current/)**    | Biblioteca con algoritmos gráficos para Neo4j       |


