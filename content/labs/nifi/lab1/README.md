# Getting Data from the Edge

**Goals**

- [ ] Explore Edge Flow Manager interface
- [ ] Monitor and manage edge MiNiFi agents

## Overview

The data that you are going to analyze is collected across several point of sales (PoS) devices your company has spread across the country. It contains account and transaction details as well as geographical coordinates of where the transactions took place.

You have several MiNiFi agents deployed across your country-wide network to collect this data where it's generated, do some processing locally and forward it to your main data center. Cloudera Edge Management is used to deploy and manage the operation of all these agents.

You need to check if things are running smoothly and your data is flowing correctly before you start analyzing the transactions.

## Tasks

!!! important
    The tasks below mention **agent-0XX**, where `XX` matches your assigned Scavenger Hunt UserID.

- Navigate to **Data Hub Clusters** and click on the `{{ efm_datahub_name | default("go01-efm--aws") }}` Data Hub cluster.

- Click on the **Edge Flow Manager UI** link to navigate into Edge Flow Manager

- Navigate to the **Flow Design** page. and find your Agent, in the end of the row, in the options select `Edit Flow`. Or double click on the line.

- Now find a way to `publish` your flow.

!!! tip
    you do not need to edit the flow we will be coming back to play with it shortly

- To view agent health, navigate to the **Monitor** page. A green check indicates that the agent is reachable and heartbeating. Clicking on a specific agent you will be able to see some agent metrics

- When checking the agents' queues we would expect that their size are zero, which means that there's no back-pressure and all the data is being processed in a timely fashion.

- To view the flow that the agent is running, go back to the **Flow Design** page and go to your specific agent.

- If an agent is not running the latest version of a flow, publish the flow via the **Flow Options** option in the top right corner and clicking **Publish**.

- Once the flow is published wait a minute or so and then review the checklist items.

!!! tip
    If you can't find the Data Hub Clusters icon, click on the "tic-tac-toe" button at the top-left corner to expand the Cloudera Management Console sidebar menu

### Checklist

- [ ]  Are all our agents healthy?
- [ ]  What's the size of the agents' queues (see tips)?
- [ ]  What's the status for the queue metrics for `agent-0XX`?
- [ ]  How many flow versions there are for `agent-0XX`?
- [ ]  Is `agent-0XX` running with the correct parameters? Are you using your agent.id?? (if not fix that !!)
- [ ]  Is `agent-0XX` running the latest flow??

**:rocket: We have now concluded Lab 2 :rocket:**
