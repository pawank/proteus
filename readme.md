# Proteus

[![Maven Central](https://img.shields.io/maven-central/v/com.cornfluence/proteus_2.12.svg)](https://maven-badges.herokuapp.com/maven-central/com.cornfluence/proteus_2.12)

ArangoDB driver for Scala.

The word 'Proteus' comes the adjective protean, with the general meaning of "versatile", "mutable", "capable of assuming many forms". "Protean" has positive connotations of flexibility, versatility and adaptability.
The name Proteus is a nod to the versatile and many-formed nature of ArangoDB.

## Getting Started

You may need to add the Sonatype nexus to your resolvers:

```
 resolvers ++= Seq("OSS" at "http://oss.sonatype.org/content/repositories/releases")
```

sbt:

```
libraryDependencies += "com.cornfluence" % "proteus_2.12" % "0.6.7"
```

maven:

```
<dependency>
  <groupId>com.cornfluence</groupId>
  <artifactId>proteus_2.12</artifactId>
  <version>0.6.7</version>
  <classifier>sources</classifier>
</dependency>
```

Note: Versions of Proteus less than 0.6.0 are for ArangoDB 2.x and built with Scala 2.11

## Configuration

To configure your application's ArangoDB user, you will need to add the following to your application.conf

```
 proteus {
   user = "username"       //arangodb default is:  "root"
   password = "password"   //arangodb default is:  ""
 }
```

## Examples

### Client API

```
            val client = DocumentClient(name = "test")

            val client = GraphClient(name = "test")
```

### Database API

Create a database:

```
            client.createDatabase("dbName", List(User(username = "user", password = "pass", active = true)))

            client.getDatabaseList

            client.getCurrentDatabase
```

Delete a database:

client.deleteDatabase("dbName")

### Collection API

```
            client.createCollection("dbName", testCollection)

            client.dropCollection("dbName", testCollection)
```

### Document API

Create a document (returning the document id as a string):

```
            client.createDocument("dbName","testCollection","""{ "Hello": "World" }""")
```

Fetch all documents:

```
            client.getAllDocuments("dbName", "testCollection")
```

Fetch a single document:

```
            client.getDocument("dbName", "testCollection", "documentID")
```

Retrieve one or more document(s) using query via AQL:

```
            client.getQueryResult("dbName", "testCollection", """{"query":"FOR u IN testCollection LIMIT 99 RETURN u", "count":true, "batchSize":2}""")
```

Retrieve one or more document(s) using query via AQL by cursor ID:

```
            client.getQueryPendingResult("dbName", "testCollection", """cursor_id""")
```

AQL examples are provided in test DocumentClientTest source file.

Update/Replace a document:

```
        client.replaceDocument("dbName", "testCollection", "documentID","""{ "Hello": "World" }""")
```

Remove a document:

```
            client.deleteDocument("dbName", "testCollection", "documentID")
```

### Graph API

(Graph API is still under some development)

Create a graph

            client.createGraph("graphName", List())

Drop a graph

            client.dropGraph("graphName")

Create a vertex collection

            client.createVertexCollection("graphName", "vertexCollectionName")

Create an edge collection

            client.createEdgeCollection("graphName", "edgeCollectionName", List("vertexCollectionName"), List("otherVertexCollectionName"))

Create a vertex

            client.createVertex("graphName", "vertexCollectionName", """{"free":"style"}""")

Create an edge

            client.createEdge("graphName", "edgeCollectionName", "typeName", "vertexOneID", "vertexTwoID")

Delete an edge

            client.deleteEdge("graphName", "edgeCollectionName", "edgeKey")

Delete an edge collection

            client.deleteEdgeCollection("graphName", "edgeCollectionName")

Delete a vertex

            client.deleteVertex("graphName", "vertexCollectionName", "vertexKey")

Delete a vertex collection

            client.deleteVertexCollection("graphName", "vertexCollectionName")
