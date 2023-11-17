---
tags:
  - postgres
---
1. Query to generate series of numbers from 1-100 with steps of 10.
  ```sql
  SELECT * FROM generate_series(1,100,10);
```

2.  Query to get the date from a series function, extract the hour as mh, format as formTime which is of the format HH12: MI AM.
   ```sql
   SELECT dt, date_part('hour',dt) As mh, to_char(dt, 'HH12:MI AM') As formtime  
FROM generate_series('2012-03-11 12:30 AM', '2012-03-11 3:00 AM', interval '15 minutes')  
As dt;
```
3.  Creating and using complex types
   ```sql
   CREATE TYPE tot_volt (r text, i text);
   CREATE TABLE circuits(circuit_id text PRIMARY KEY, tot_volt complex_number);
   INSERT INTO circuits (tot_volt) VALUE (ROW(1,2));
   SELECT tot_volt.r, tot_volt.i FROM circuits;
```
4. Specifying the op class for var char index
   ```sql
   CREATE INDEX idx_bt_my_table_description_varchar_pattern ON my_table  
USING btree (description varchar_pattern_ops);
```

5. Case insensitive indexes can be created as follows
   ```sql
   CREATE INDEX idx_featnames_ufullname_varops ON featnames_short  
USING btree (upper(fullname) varchar_pattern_ops);
```
6. Query to create a new database
   ```sql
   CREATE DATABASE test;
```