# Guide for Producing and Exploring Knowledge Graphs using Cypher
## N-Triples and Knowledge Graphs Instructions
These files in this directory of the biomarker project will demonstrate how to take a N-Triples data format and convert it in a knowledge graph using Neo4j
## Neo4j Installation
1. Download and install Neo4j from these instructions: [Neo4j installation](https://neo4j.com/docs/desktop-manual/current/installation/download-installation).
2. Move the **apoc-5.15.0-cor.jar** file from ***'C:\\...\\.Neo4jDesktop\\relate-data\\dbmss\\name_of_dbms\\labs*** to ***C:\\...\\.Neo4jDesktop\\relate-data\\dbmss\\name_of_dbms\\plugins***
3. In the ***C:\\...\\.Neo4jDesktop\\relate-data\\dbmss\\name_of_dbms\\conf\\neo4J.conf*** file, add the following line:
   
   _dbms.unmanaged_extension_classes=n10s.endpoint=/rdf_

4. (Optional) Add a file named **apoc.conf** to the ***C:\\...\\.Neo4jDesktop\\relate-data\\dbmss\\name_of_dbms\\conf*** directory that contains the following lines:
   
   _apoc.import.file.enabled=true_
   
   _apoc.import.file.parallel.enabled=true_

**For detailed instructions of APOC and Neoseamtics (n10s) plugin installation**: [APOC installation](https://neo4j.com/labs/apoc/4.1/installation/) and [Neosemantics installation](https://neo4j.com/labs/neosemantics/installation/).
   
## Neo4j Setup
1. Open up Neo4J desktop and create a new project.
2. Add a new DBMS
3. Click on your DBMS and on the right a panel will show up with Details, Plugins, and Upgrade
4. Click on Plugins and install APOC and Neosemantics (n10s) plugins (Ensure plugins are compatible)
![Plugins_img](https://github.com/MiguelMazumder/csci_6221_Solidity/assets/72771218/81ab3589-ccab-425c-80a7-4413a1b6bbb1)

## Produce a Knowledge Graph from N-Triples
1. Click on your DBMS again and start it, once started click the open tab for a neo4j browser
2. Ensure APOC and Neosemantics (n10s) were function properly by executing command "***SHOW PROCEDURES***"
   There should be apoc, dbms, and n10s procedures. (If only dbms procedures are available, perform optional step 4 of Neo4J installation)
4. Run this query:

   ***CREATE CONSTRAINT n10s_unique_uri FOR (r:Resource) REQUIRE r.uri IS UNIQUE***

  *The n10s_unique_uri constraint is used in the context of the NeoSemantics (n10s) plugin for Neo4j when working with RDF data. This constraint ensures that URIs     (Uniform Resource Identifiers) used in RDF data are unique among nodes of type Resource in the Neo4j graph. This line only needs to be executed once and will       remain until you explicitly remove the constraint (_DROP CONSTRAINT n10s_unique_uri;_)

5. Next, run these two queries (Ensure backslashes are consistent with operating system: 
   ***ALL n10s.graphconfig.init();
   CALL n10s.rdf.import.fetch("file:///Address_of_nt_file.nt", "N-Triples");***

## Sample Queries from Knowledge graph
To execute a query on the knowledge graph using Cypher, an example is provided for an understanding of how it works

***MATCH (startNode)-[r]-(endNode);***

***WHERE endNode.uri = 'http://purl.obolibrary.org/obo/UBERON_0000178'***

***RETURN startNode, r, endNode;***

This query retrieves patterns in the graph where there is a relationship between startNode and endNode, and the endNode has a specific URI value. It then returns the relevant nodes and relationship information for those patterns. In this case, the URI value is entity type blood, hence nodes pointing to the specified node will be biomarkers that are found from blood samples
