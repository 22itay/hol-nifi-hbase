# AI with NiFi DataFlow

**Goals**

- [ ] Deploy NiFi DataFlow to intecept Fraud Transactions
- [ ] Process transaction data through an AI model
- [ ] Configure Kafka topics for AI-enhanced data pipeline

## Overview

This has been great. Our Cyber Team was able to flag fraud transactions with "xxx" on the transaction_id.  Now we can investigate further to confirm whether they are actually fraud. Good job team!

Our Principal Data Scientist has come up with a new AI workflow that is able to give us some insights from the transaction data itself. Let's use Data Flow to create a new topic which we can pass all these fraud transactions to our Data Science Team.

## Tasks

!!! important
    The tasks below mention `<your workshop username>`. This should be your assigned unique username used to access the Cloudera on cloud tenant.

1. Click on the **Catalog** menu in Data Flow.
1. Select the flow called **Edge2AI-Fraud-Transaction**
   1. Click on **Deploy** in the details pane
      1. In the New Deployment dialog:
         1. **Target Workspace**: `{{ cdf_workspace_name | default('go01-demo-aws') }}`
      1. In the **Overview** page:
         1. **Deployment Name**: `<your workshop username> AI Fraud`
         2. **Target Project:** Select the option `Unassigned`
      1. In the **Nifi Configuration** page:
         1. **Nifi Runtime:**  `Nifi 2.x`
      1. In the **Parameters** page:
         1. **Filter Rule**: `SELECT * FROM FLOWFILE WHERE transaction_id LIKE 'xxx%'` 
         1. **Consumer Group ID**: `fraud-consumer-<Scavenger_Hunt_UserID>`
         1. **Source Topic**: `edge-data-<Scavenger_Hunt_UserID>`
         1. **Target Topic**: `fraud-topic-<Scavenger_Hunt_UserID>`
         1. **Workload Username**: `<your workshop username>`
         1. **Workload Password**: `<your workshop password>`
         1. Leave remaining parameters in the *pla-parameter Group*  as is
      1. In the **Sizing & Scaling** page:
          1. **NiFi Node Sizing**: `extraSmall`
          2. **Auto Scaling**: `disabled`
          3. **Storage Selection**: `Standard`
      1. In the **Key Performance Indicators** click **Next**.
   1. Click on **Deploy** to start the flow execution
   1. Check the deployed flow details
   1. Click on **Action > Manage Deployment** to see more information

### Tips

* The NiFi deployment is being created and should complete in 2-3 minutes. If it takes longer or errors out, please let the instructors know.

* Once the deployment has completed, it will take a few seconds for the Data Received/Sent gauge to be updated. You can now explore the deployment to complete the remaining tasks of this section. Explore the NiFi UI and the Deployment Manager.


### Checklist

- [ ] Deploy the **Edge2AI-Fraud-Transaction** flow from the Catalog
- [ ] What's the processor used on the flow to filter fraud transactions?
- [ ] Check the target topic in Streams Messaging Manager to confirm it is all fraud transactions.

**:rocket: We have now concluded Lab 7 :rocket:**

**:rocket: This concludes our Hands on Workshop :rocket:**
