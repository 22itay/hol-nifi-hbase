# Query the optimized tables data

**Goals**

- [ ] Login to HUE 
- [ ] Query the Tables data and understand what happens behind the scenes


## Overview

We will run some queries in order to check efficiency 

## Tasks

!!! important
    The tasks below mention **user-0XX**, where `XX` matches your assigned Scavenger Hunt UserID.

- Connect to HUE (URL)


- Check data is loaded to the table


```sql
SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> LIMIT 100;
```

- Check efficiency of select by SENSOR_ID

```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> WHERE SENSOR_ID='SENSOR_007' LIMIT 100;
```

- Check efficiency of select by STATUS_MSG


```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> WHERE STATUS_MSG='LOW_VOLTAGE' LIMIT 100;
```

So if we have created an index why are we still perfroming a full table scan??

Index table only maps the column indexed and the primary key only
How can we solve this problem?

- Query also primary key

```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> WHERE STATUS_MSG='LOW_VOLTAGE' AND SENSOR_ID='SENSOR_007' LIMIT 100;
```

- Now lets try the same on the old table to see the diference
```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> WHERE STATUS_MSG='LOW_VOLTAGE' AND SENSOR_ID='SENSOR_007' LIMIT 100;
```


So what else can we do if we also want to have another column queried with the STATUS_MSG?

- Add a hint for the table to use the index
```sql
SELECT 
/*+ INDEX(SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> IDX_STATUS) */ 
*
FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> 
WHERE STATUS_MSG = 'LOW_VOLTAGE'
LIMIT 100;
```

We can also create a covered index that will contain another column's data

- Lets create another table with a covered index using also the column READING and populate it

```python


print("\n[Step 3] Creating Optimized Table...")
# Optimization: Lead with SENSOR_ID, add Salt Buckets, and Compression.
cursor.execute("""
        CREATE TABLE IF NOT EXISTS SENSORS_<userxxx>.SENSOR_DATA_COVERED_<userxxx> (
            SENSOR_ID VARCHAR NOT NULL,
            EVENT_TIME TIMESTAMP NOT NULL,
            READING DOUBLE,
            STATUS_MSG VARCHAR,
            CONSTRAINT pk PRIMARY KEY (SENSOR_ID, EVENT_TIME)
        ) SALT_BUCKETS = 8, COMPRESSION = 'GZ'
""")
cursor.execute("CREATE INDEX IDX_STATUS_COVERED ON SENSORS_<userxxx>.SENSOR_DATA_COVERED_<userxxx> (STATUS_MSG) INCLUDE (READING)")
print(" Migrating data internally (UPSERT SELECT)...")
# This moves data server-side without pulling 50k rows to Python.
start_mig = time.time()
cursor.execute("""
        UPSERT INTO SENSORS_<userxxx>.SENSOR_DATA_COVERED_<userxxx> (SENSOR_ID, EVENT_TIME, READING, STATUS_MSG)
        SELECT SENSOR_ID, EVENT_TIME, READING, STATUS_MSG FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx>
""")
print(f"  Migration finished in {time.time() - start_mig:.2f}s")


```

- And now we don't need to use the hint (be aware that if we had more columns they won't be covered)

```sql
Explain SELECT *
FROM SENSORS_<userxxx>.SENSOR_DATA_COVERED_<userxxx>
WHERE STATUS_MSG = 'LOW_VOLTAGE'
LIMIT 100;
```



Skip scan 

The Skip Scan leverages SEEK_NEXT_USING_HINT of HBase Filter. It stores information about what set of keys/ranges of keys are being searched for in each column. It then takes a key (passed to it during filter evaluation), and figures out if it's in one of the combinations or ranges or not. If not, it figures out which next highest key to jump.


```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_ADVANCED_<userxxx> WHERE SENSOR_ID IN ('SENSOR_001', 'SENSOR_007');
```

Local indexes 
 
Local indexes are better for write-heavy tables because the index data lives on the same RegionServer as the actual data, reducing network traffic.

```sql
CREATE LOCAL INDEX IDX_LOCAL_STATUS ON SENSORS_<userxxx>.SENSOR_DATA_COVERED_<userxxx> (STATUS_MSG);
```

If data alraedy exists in the table we can create an async index and than populate the data using a mapreduce

for example : 

${HBASE_HOME}/bin/hbase org.apache.phoenix.mapreduce.index.IndexTool
  --schema MY_SCHEMA --data-table MY_TABLE --index-table ASYNC_IDX
  --output-path ASYNC_IDX_HFILES




**:rocket: We have now concluded Lab 4 :rocket:**
