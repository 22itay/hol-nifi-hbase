# Receiving edge data with Data Flow

**Goals**

- [ ] Verify data flowing from edge MiNiFi agents to the Cloudera Data Flow deployment
- [ ] Examing utlization and statistics of the deployed flow
- [ ] Become familar with the components that make up the Data Flow

## Overview

The flow that is being executed by the MiNiFi agents forward the data to a Data Flow, running in your Cloudera Public Cloud environment. Now that you have verified that your agents are running fine and sending data, check the Data Flow deployment to make sure that the data is being received successfully.

## Tasks

!!! warning
    Do not make ANY changes to the "Receive Edge Data" flow. This flow is shared with everybody in the workshop

* Navigate to **Cloudera Data Flow**

* To check the flows that are currently executing, click on the **Deployment** menu

* Click on the **Receive Edge Data** deployment to see its details

* In the deployment details tab, click on **Actions > View in NiFi**.

!!! tip
    If you can't find the Cloudera Data Flow icon icon, click on the "tic-tac-toe" button at the top-left corner to expand the Cloudera Management Console sidebar menu

### Checklist

- [ ] Is the production flow ***Receive Edge Data*** deployed and running healthily?
- [ ] Does this send data out? If so, what's the average throughput for data sent?
- [ ] What's the average CPU and memory utilization for this flow?
- [ ] How many processors are there in this flow and what do they do? (see tips)

**:rocket: We have now concluded Lab 4 :rocket:**
