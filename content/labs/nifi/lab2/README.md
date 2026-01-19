# Managing Schemas with Schema Registry

**Goals**

- [ ] Understand the role of Schema Registry in data pipeline architecture
- [ ] Locate, examine and Verify the FinTransactions schema in Schema Registry

## Overview

Well, it looks like we're receiving data from the edge as expected. So let's move on to the next step in our pipeline.

In the next sections, we'll continue to process the data and will have to access specific fields contained in the transaction payload. For that, applications need to know what's the structure of that data and they use "Schemas" for that. Schemas are simply a description of the data structure that all applications can use as a contract to exchange information.

We have a schema already defined for the transaction data we are using and it has been registered centrally in our Schema Registry so that all applications can access and use the same schema.

Before we start processing the data in the next step, let's check if everything is ok with the schema information.

## Tasks

- Navigate to **Data Hub Clusters** and click on the `{{ smm_datahub_name | default("cdf-aw-kafka-demo") }}` Data Hub cluster.

- Click on the **Schema Registry** link to navigate into Schema Registry

- The name of the schema we'll be using is **FinTransactions**.

- Try creating a schema to see the different options you can specify.

- Navigate to **Data Hub Clusters** and click on the `{{ smm_datahub_name | default("cdf-aw-kafka-demo") }}` Data Hub cluster.

- Click on the **Streams Messaging Manager** link to navigate into SMM.

- Find your topic name `edge-data-0XX` and click on it to see its partitions.

- Click on any of the partitions and then "Explore" to browse its data. 


!!! tip
    If you can't find the Data Hub Clusters icon, click on the "tic-tac-toe" button at the top-left corner to expand the Cloudera Management Console sidebar menu

### Checklist
#### Schema Registry

- [ ] What's the compatibility type set for the `FinTransactions` schema?
- [ ] What are the different options for compatibility when creating a new schema?
- [ ] What are the data types of the `lat` and `long` columns?

#### Streams Messaging Manager
- [ ] How many partitions does the `edge-data-0XX` topic have?
- [ ] What is the configured replication factor? Minumum in-sync replicas?

**:rocket: We have now concluded Lab 3 :rocket:**
