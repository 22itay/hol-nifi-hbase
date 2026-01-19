# Optimizong HBase tables

**Goals**

- [ ] Create the new HBase table that will get better performance
- [ ] Loading the data from the old table 
- [ ] Creating index over the data
- [ ] Understanding range scans

## Overview

We will create a new table that fits our queries in order to improve performance

## Tasks


!!! important
    The tasks below mention **user-0XX**, where `XX` matches your assigned Scavenger Hunt UserID.
    All Python code will run on CAI

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


url = "<phoenix python url>"

print("Connecting to Cloudera Phoenix...")
conn = phoenixdb.connect(url, autocommit=True, **opts)
cursor = conn.cursor()
```

- create the new table

- We added here slat buckets , compression and changed primary key order to get better performance over SENSOR_ID scanning 

```python
print("\n[Step 3] Creating Optimized Table...")
    # Optimization: Lead with SENSOR_ID, add Salt Buckets, and Compression.
    
cursor.execute("""
    CREATE TABLE IF NOT EXISTS SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> (
            SENSOR_ID VARCHAR NOT NULL,
            EVENT_TIME TIMESTAMP NOT NULL,
            READING DOUBLE,
            STATUS_MSG VARCHAR,
            CONSTRAINT pk PRIMARY KEY (SENSOR_ID, EVENT_TIME)
        ) SALT_BUCKETS = 8, COMPRESSION = 'GZ'
    """)
```

- Now lets build our index for scanning over STATUS_MSG and populate the data

```python

cursor.execute("CREATE INDEX IF NOT EXISTS IDX_STATUS ON SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> (STATUS_MSG)")
print("[Step 4] Migrating data internally (UPSERT SELECT)...")
# This moves data server-side without pulling 50k rows to Python.
start_mig = time.time()
cursor.execute("""
        UPSERT INTO SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> (SENSOR_ID, EVENT_TIME, READING, STATUS_MSG)
        SELECT SENSOR_ID, EVENT_TIME, READING, STATUS_MSG FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx>
    """)
print(f"  Migration finished in {time.time() - start_mig:.2f}s")
```



### Checklist

- [ ]  Can we see data in the new table?

**:rocket: We have now concluded Lab 3 :rocket:**
