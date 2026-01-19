---
hide:
  - toc
---
# Cloudera Hbase NiFi Hands on Lab

The goal of this workshop is to have fun!!!

!!! info "What to expect"
    This scavenger hunt Hands on Lab challenges you to understand a real-time fraud detection system built on Cloudera's leading data stack.


    Good time!

## The Stack Today

* **Hbase**: Column-oriented NoSQL datastore that provides real-time, random read/write access ontop HDFS
* **Phoenix**: Enables low-latency SQL querying and OLTP applications directly on top of HBase
* **HUE**: Web interface and SQL assistant that simplifies querying, analyzing, and managing data.
* **MiNiFi**: Generates synthetic transaction events and routes them to Kafka.
* **Edge Flow Manager (EFM)**: Manages the entire fleet of deployed MiNiFi agents.
* **DataFlow/NiFi**: Copy transaction events from edgeTopic to fraudulent Topic for further analysis
* **Schema Registry**: Stores and manages the schema for transaction events.
* **Kafka**: Receives and distributes transaction events to consumers.

![Hands on Lab Flow Overview](./assets/images/data-in-motion-diagram.webp)


!!! tip
    Use the workshop instructions to follow the flow, but also use the time to explore the product and learn new things and tricks. We expect you to be more confident with the product and lead workshops with customers with what you learn here today.

<div class="grid cards"  markdown>

- :simple-cloudera:{ .lg .middle } &nbsp; **welcome. Access Cloudera Environment**

    ***

    **Goals**

    - [ ] Use Case Overview
    - [ ] Connect to Cloudera on cloud control plane

    ***

    [:octicons-arrow-right-24: Go to Lab 0 Guide](labs/lab0/README.md)

- :simple-cloudera:{ .lg .middle } &nbsp; **Lab 1. hbase all the way**

    ***

    **Goals**

    - [ ] Explore Edge Flow Manager interface
    - [ ] Monitor and manage edge MiNiFi agents

    ***

    [:octicons-arrow-right-24: Go to Hbase Lab Guide](labs/hbase/README.md)

- :simple-cloudera:{ .lg .middle } &nbsp; **Lab 2. NIFI - Edge to AI**

    ***

    **Goals**

    - [ ] Explore Edge Flow Manager interface
    - [ ] Monitor and manage edge MiNiFi agents

    ***

    [:octicons-arrow-right-24: Go to NiFi Lab Guide](labs/nifi/README.md)

</div>
