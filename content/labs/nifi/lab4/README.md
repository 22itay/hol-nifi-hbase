# Moving Data with NiFi DataFlow

**Goals**

- [ ] Configure and deploy a flow from the Flow Catalog
- [ ] Monitor flow performance using KPIs to ensure data isn't backing up in the pipeline
- [ ] Verify end-to-end data flow from edge data topic to fraud analysis topic in Streams Messaging Manager

## Overview

So lets move on to the next step in our pipeline: moving data into Kafka topics that will feed our fraud analytics application. We have already designed a flow for taking care of this but it's not running yet. It is stored securely in the central flow catalog. Let's deploy it and get it running.

## Tasks

!!! important
    The tasks below mention `<your workshop username>`. This should be your assigned unique username used to access the Cloudera on cloud tenant.

1. Click on the **Catalog** menu in Data Flow.
2. Select the flow called **Kafka-To-Kafka TxN for Fraud analysis With ParamGroup**
   1. Click on **Deploy** in the details pane
      1. In the New Deployment dialog:
         1. **Target Workspace**: `{{ cdf_workspace_name | default("go01-demo-aws") }}`
      1. In the **Overview** page:
         1. **Deployment Name**: `<your workshop username> fraud flow`
         2. **Target Project:** Select the option `Unassigned`
      2. In the **Nifi Configuration** page:
         1. **Nifi Runtime:**  `Nifi 2.x`
      3. In the **Parameters** page:
         1. **CDP Workload User**: `<your workshop username>`
         2. **CDP Workload User Password**: `<your workshop password>`
         3. **Filter Rule**: `SELECT * FROM FLOWFILE`
         4. **Kafka Destination Topic**: `fraudulent-data-<Scavenger_Hunt_UserID>`
         5. **Kafka Producer ID**: `producer-<Scavenger_Hunt_UserID>`
         6. **Kafka Source Topic**: `edge-data-<Scavenger_Hunt_UserID>`
         7. **Kafka consumer Group ID**: `consumer-<Scavenger_Hunt_UserID>`
         8. **Schema Name**: `FinTransactions`
         9. Leave remaining parameters in the *pla-parameter Group*  as is
      4. In the **Sizing & Scaling** page:
         1. **NiFi Node Sizing**: `extraSmall`
         2. **Auto Scaling**: `disabled`
         3. **Storage Selection**: `Standard`
      5. In the **Key Performance Indicators** page add a new KPI:
         1. **KPI Scope**: `Entire Flow`
         2. **Metric to Track**: `Flow Files Queued` (This KPI will show you whether data is backing up in the flow)
         3. **Trigger alert when metric is greater than**: `100`
         4. **Alert will be triggered when metric is outside the boundary(s) for**: `5 minutes`
      6. Click the **Deploy** button to start the flow execution.
   2. Check the deployed flow details
   3. Click on **Action > Manage Deployment** to see more information

### Tips

* The NiFi deployment is being created and should complete in 2-3 minutes. If it takes longer or errors out, please let the instructors know.

* Once the deployment has completed, it will take a few seconds for the Data Received/Sent gauge to be updated. You can now explore the deployment to complete the remaining tasks of this section. Explore the NiFi UI and the Deployment Manager.

### Checklist

- [ ] Deploy the **Kafka-To-Kafka TxN for Fraud analysis With ParamGroup** flow from the Catalog
- [ ] What is the number of flow files queued for your running deployment?
- [ ] What is the actual value for the **Data Input Format** and **Data Output Format** parameters for the running deployment?
- [ ] What's the topic name that the new flow deployment is writing to?
- [ ] Can you see new data coming into this topic in Streams Messaging Manager?

**:rocket: We have now concluded Lab 5 :rocket:**
