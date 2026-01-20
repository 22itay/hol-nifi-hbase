# Loading data to HBase

**Goals**

- [ ] Create the Phoenix connection
- [ ] Creating your **first** table
- [ ] Loading dummy data into the table

## Overview

You need to check if things are running smoothly
In order to do it we can connect to hbase shell.

## Tasks

First we would go to your user profile and create a Workload Password and SSH access key


!!! important
    The tasks below mention **user-0XX**, where `XX` matches your assigned Scavenger Hunt UserID.
    All Python code will run on CAI

 - Install phoenixdb
```python
!pip install phoenixdb
```

- create the Phoenix connection

```python
import phoenixdb
import phoenixdb.cursor
from datetime import datetime
import random
import time
import urllib3

# 1. SETUP & AUTHENTICATION
# Suppress SSL warnings for lab environments
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Replace with your specific Cloudera Workload Credentials
opts = {
    'authentication': 'BASIC',
    'user': '<User>', 
    'password': '<WL Pasword>',
    'verify': False 
}


url = "https://cod-1eevbst1maraf-gateway.cldr-gre.yovj-8g7d.cloudera.site/cod-1eevbst1maraf/cdp-proxy-api/avatica/"

print("Connecting to Cloudera Phoenix...")
conn = phoenixdb.connect(url, autocommit=True, **opts)
cursor = conn.cursor()
```

- Creating your **first** table
 - This table will be holding a primary key with EVENT_TIME and SENSOR_ID


```python
   print("\n[Step 1] Creating Naive Table...")
    # Design Flaw: Leading with Time causes write hotspots and slow sensor searches.
cursor.execute("""CREATE SCHEMA IF NOT EXISTS SENSORS_<userxxx>""")

    
cursor.execute("""
        CREATE TABLE IF NOT EXISTS SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> (
            EVENT_TIME TIMESTAMP NOT NULL,
            SENSOR_ID VARCHAR NOT NULL,
            READING DOUBLE,
            STATUS_MSG VARCHAR,
            CONSTRAINT pk PRIMARY KEY (EVENT_TIME, SENSOR_ID)
        )
    """)
```

- Loading dummy data into the table:

```python
print("[Step 2] Loading 50,000 rows into Naive Table (Batching 500)...")
batch_size = 200
sensors = [f'SENSOR_{i:03}' for i in range(1, 51)]
errors = ["OK", "CONNECTION_TIMEOUT", "LOW_VOLTAGE", "SENSOR_STUCK"]
    
data_to_insert = []
for i in range(1, 50001):
    row = (datetime.now(), random.choice(sensors), random.uniform(20, 90), random.choice(errors))
    data_to_insert.append(row) 
    if i % batch_size == 0:
        cursor.executemany("UPSERT INTO SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> VALUES (?, ?, ?, ?)", data_to_insert)
        data_to_insert = []
        if i % 1000 == 0: print(f"  Progress: {i}/50000...")
```

### Checklist

- [ ]  Are all our tables healthy?

**:rocket: We have now concluded Lab 1 :rocket:**
