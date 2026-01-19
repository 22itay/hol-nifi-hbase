# Query the tables data

**Goals**

- [ ] Login to HUE 
- [ ] Query the Tables data and understand what happens behind the scenes


## Overview

We will run some queries in order to check efficiency 

## Tasks

!!! important
    The tasks below mention **user-0XX**, where `XX` matches your assigned Scavenger Hunt UserID.

- Connect to HUE (https://cod-1eevbst1maraf-gateway.cldr-gre.yovj-8g7d.cloudera.site/cod-1eevbst1maraf/cdp-proxy/hue/hue)


- Check data is loaded to the table


```sql
SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> LIMIT 100;
```

- Check eficciency of select by SENSOR_ID

```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> WHERE SENSOR_ID='SENSOR_007' 
```

- Check eficciency of select by STATUS_MSG


```sql
EXPLAIN SELECT * FROM SENSORS_<userxxx>.SENSOR_DATA_NAIVE_<userxxx> WHERE STATUS_MSG='LOW_VOLTAGE' LIMIT 100;
```

### Checklist

- [ ]  Can you explain why we have a full table scan?

**:rocket: We have now concluded Lab 2 :rocket:**
