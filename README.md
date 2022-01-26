> Load Hop and other lineage data to Neo4j

# (Meta)data Lineage in Neo4j through Apache Hop 
![](https://img.shields.io/badge/status-active-brightgreen)
![](https://img.shields.io/badge/hop-v0.99-blue)
![](https://img.shields.io/badge/neo4j-v4.3.6-blue)
![](https://img.shields.io/badge/Maintained%3F-yes-green.svg)

Data lineage information is an indispensable part of data engineering projects. This repository provides a start to parsing your lineage information in a Neo4j graph database using Apache Hop. 

> :warning: This repository is work in progress. Some areas of the code have been [ported]() and may be largely untested.    
> :warning: This repository currently runs a scheduled (batch) import of your infrastructure and data integration code. Apache Hop will gradually include more built-in lineage functionality    

The areas this project covers currently are: 

* AWS infrastructure (json based)
* GCP (BigQuery)
* data integration (Apache Hop) workflows and pipelines
* Git (commit history)
* Pentaho (prpt reports, mondrian, analyzer)
* RDBMS (database, schema, table, column)

# Loading your lineage data to Neo4j 

[Download](https://hop.apache.org/download/download/) a recent Apache Hop release build and unzip   

[Download](https://github.com/mattcasters/hop-neo4j/releases) the Neo4j Hop plugins, unzip to `hop/plugins/transforms`

Clone this repository: 

<code>git clone https://github.com/knowbi/knowbi-hop-meta-to-neo4j.git</code>

Copy `project-config.json.template` to `project-config.json` and change the variables (in the json file or through Hop Gui): 

|Name|Value|Description (optional information)|
|----|-----|----------------------------------|
|NEO4J_COMM_HOST||	
|NEO4J_COMM_BOLT_PORT|7687||	
|NEO4J_COMM_BROWSER_PORT|7474||	
NEO4J_COMM_USER|neo4j||
|NEO4J_COMM_PASS|||	
|do.aws|Y|include AWS infrastructure?|
|do.aws.dms|N|nclude AWS DMS (depends on do.aws)|
|do.aws.rds|N|include AWS RDS (depends on do.aws)|
|do.clean.neo4j.data|Y|clean Neo4j database before running (DELETES **EVERYTHING**!!)|
|do.etl|Y|include Hop ETL parsing?|
|do.gcp|N|include GCP infrastructure (BigQuery only for now)|
|do.git|Y|include git commit history?|
|do.pentaho|N|include Pentaho reports and cubes?|
|do.pentaho.report|N|include Pentaho reports (depends on do.pentaho)?|
|do.pentaho.mondrian.schema|N|include Pentaho/Mondrian schemas and cubes (depends on do.pentaho)?|
|do.rdbms|N|include RDBMS schema parsing?|
|do.rdbms.columns|Y|include columns in RDBMS schema parsing (if 'N', only database, schema, table parsing)
|git.tmp.dir|/tmp|temporary directory to store git parsing working files|
|etl.kettle.properties.dir||directory to read kettle.properties file from (deprecated)|
|etl.dir|/customer/project/directory|directory to read Hop workflows and pipelines from|
|neo4j.host|localhost|Neo4j database host|
|neo4j.bolt.port|7687|Neo4j bolt port (default 7687)|
|neo4j.browser.port|7474|Neo4j browser port (default 7474)|
|neo4j.user|neo4j|Neo4j username (default neo4j)|
|neo4j.pass|knowbi|Neo4j password|
|pentaho.mondrian.analyzer.dir||Pentaho Analyzer reports directory|
|pentaho.mondrian.properties.dir||mondrian.properties path|
|pentaho.mondrian.schema.dir||Pentaho Mondrian schema files directory|
|pentaho.report.dir||Pentaho Reports (prpt) directory|
