## Views.

Views can be created using the following query.
```sql 
CREATE OR REPLACE VIEW census.vw_facts AS  
SELECT lf.fact_type_id, lf.category, lf.fact_subcats, lf.short_name  
, f.tract_id, f.yr, f.val, f.perc  
FROM census.facts As f  
INNER JOIN census.lu_fact_types As lf  
ON f.fact_type_id = lf.fact_type_id;
```

The above query creates a  view called `vw_facts` by joining the tables `lu_fact_types` and `facts`.
## Triggers.
Row level & statement level triggers.
Row level triggers run for each row. Statement level trigger will run only once.

The above view can be updated by using a trigger. The following PL/pgSQL function will act as the trigger.
```sql
CREATE OR REPLACE FUNCTION census.trig_vw_facts_ins_upd_del() RETURNS trigger AS  
$$  
BEGIN  
IF (TG_OP = 'DELETE') THEN  
DELETE FROM census.facts AS f  
WHERE f.tract_id = OLD.tract_id AND f.yr = OLD.yr AND f.fact_type_id =  
OLD.fact_type_id;  
RETURN OLD;  
END IF;  
IF (TG_OP = 'INSERT') THEN  
INSERT INTO census.facts(tract_id, yr, fact_type_id, val, perc)  
SELECT NEW.tract_id, NEW.yr, NEW.fact_type_id, NEW.val, NEW.perc;  
RETURN NEW;  
END IF;  
IF (TG_OP = 'UPDATE') THEN  
IF ROW(OLD.fact_type_id, OLD.tract_id, OLD.yr, OLD.val, OLD.perc)  
!= ROW(NEW.fact_type_id, NEW.tract_id, NEW.yr, NEW.val, NEW.perc) THEN  
UPDATE census.facts AS f  
SET tract_id = NEW.tract_id, yr = NEW.yr  
, fact_type_id = NEW.fact_type_id  
, val = NEW.val, perc = NEW.perc  
WHERE f.tract_id = OLD.tract_id  
AND f.yr = OLD.yr  
AND f.fact_type_id = OLD.fact_type_id;  
RETURN NEW;  
ELSE  
RETURN NULL;  
END IF;  
END IF;  
END;  
$$  
LANGUAGE plpgsql VOLATILE;
```

#### General Information:

- The function is named `census.trig_vw_facts_ins_upd_del`.
- It returns a `trigger`.
- The function is defined as `VOLATILE`, meaning it can have side effects and its result for a given input might change across multiple calls.

#### Function Body:

1. **Handling DELETE Operations**:
    - The function checks if the operation (`TG_OP`) that invoked the trigger was a `DELETE`.
    - If it was, it deletes records from the `census.facts` table where the `tract_id`, `yr`, and `fact_type_id` match the old values (i.e., the values of the row that was deleted).
    - After performing the deletion, the function returns the `OLD` record.
2. **Handling INSERT Operations**:
    - The function checks if the operation that invoked the trigger was an `INSERT`.
    - If it was, it inserts a new record into the `census.facts` table with the values of `tract_id`, `yr`, `fact_type_id`, `val`, and `perc` from the `NEW` record (i.e., the values of the row that was inserted).
    - After performing the insertion, the function returns the `NEW` record.
3. **Handling UPDATE Operations**:
    - The function checks if the operation that invoked the trigger was an `UPDATE`.
    - Within this, the function checks if the old values of `fact_type_id`, `tract_id`, `yr`, `val`, and `perc` are different from the new values. This determines if any relevant column has been changed.
    - If the values are different (i.e., at least one column was updated):
        - The function updates the record in the `census.facts` table where the `tract_id`, `yr`, and `fact_type_id` match the old values.
        - The new values from the `NEW` record are set in the `census.facts` table.
        - After performing the update, the function returns the `NEW` record.
    - If the values remain the same (i.e., no relevant column was updated), the function simply returns `NULL`.
#### Additional Notes:

- In the context of a trigger function, `NEW` and `OLD` are special variables.
    - `NEW` contains the new row values during `INSERT` and `UPDATE` operations.
    - `OLD` contains the old row values during `UPDATE` and `DELETE` operations.

In summary, this function is a trigger function that performs different actions based on the type of operation (INSERT, UPDATE, DELETE) that invoked the trigger. It ensures that the `census.facts` table is kept in sync based on these operations, handling each case specifically.

### Binding the trigger.
The above trigger can be bound to the view as shown below.
```sql 
CREATE TRIGGER trip_01_vw_facts_ins_upd_del INSTEAD OF INSERT OR UPDATE OR DELETE ON census.vw_facts FOR EACH ROW EXECUTE PROCEDURE census.trig_vw_facts_ins_upd_del();
```
### BEFORE, AFTER & INSTEAD OF
Instead of triggers are used instead of the normal action. They can only be used with views. Before & After triggers can only be used with tables.

A trigger function  never takes a literal input argument though internally they have access to the trigger  state data and can modify it. They always output a datatype called a trigger. Because  PostgreSQL trigger functions are just another function, you can reuse the same trigger  function across different triggers. To apply multiple triggering functions, you must create  multiple triggers against the same event.

*Example 8-9. Trigger function to timestamp new and changed records*  
```sql
-- Create trigger function.
CREATE OR REPLACE FUNCTION trig_time_stamper() RETURNS trigger AS  
$$  
BEGIN  
NEW.upd_ts := CURRENT_TIMESTAMP;  
RETURN NEW;  
END;  
$$
LANGUAGE plpgsql VOLATILE; 
-- Bind trigger here.
CREATE TRIGGER trig_1  
BEFORE INSERT OR UPDATE OF session_state, session_id  
ON web_sessions  
FOR EACH ROW  
EXECUTE PROCEDURE trig_time_stamper();  
```
1. Define the trigger function. This function can be used on any table that has a  
upd_ts column . It changes the value of the upd_ts field of the new record before  
returning. Trigger functions that change values of a row should only be called in the  
BEFORE event, because in the AFTER event, all updates to the NEW record will be ignored.  
2. The trigger will fire before the record is committed.  
3. This is a new feature introduced in PostgreSQL 9.0+ that allows us to limit the firing  
of the trigger only if specified columns have changed. In prior versions, you would  
do this in the trigger function itself using a series of comparison between OLD.some_column and NEW.some_column. This feature is not supported for INSTEAD  
OF triggers.
4. Bind the trigger to the table.
## Window Functions.
A window function has the unusual knack to see and use data beyond the current  
row, hence the term window. Without window functions, you’d have to resort to using  
joins and subqueries to poll data from adjacent rows. On the surface, window functions  
do violate the set-based operating principle of SQL, but we mollify the purist by claim-  
ing them to be a short-hand.
```sql
SELECT tract_id, val, AVG(val) OVER () as val_avg  
FROM census.facts WHERE fact_type_id = 86;
```
It returns the tract_id along with the current value and the average value.

<mark style="background: #FAE45054;">When PostgreSQL sees a window function in a particular row,  
it will actually scan all rows fitting the WHERE clause, perform the aggregation, and output  
the value as part of the row</mark>

They also allow an order by clause. Partition can be used along with the order by as shown in the following query.
```sql
SEKECT tract_id, val, AVG(val), OVER (PARTITION BY left(tract_id, 5) ORDER BY val) AS avg_county_ordered FROM census.facts
WHERE fact_type_id = 86 ORDER BY left(tract_id,5), val;
```

### PARTITION BY
`PARTITION BY` is used to partition the rows into separate windows. <mark style="background: #FFDE0080;">This  
instructs PostgreSQL to subdivide the window into smaller panes and then to take the  
aggregate over those panes instead of over the entire set of rows.</mark>

### LAG & LEAD
As the name implies they are used to find leading and lagging rows.
They can be invoked as shown below
`LAG(column_name, <optional-step-value>) OVER ()`

Other window functions include
MIN, MAX, AVG, SUM etc.

## Common Table Expressions.
They allow you to assign a temp variable name to  a query def so that it can be used in a larger query. 
There are three diff ways to CTEs:
1.  **Standard  CTE**s:  Non recursive, non-writable. Sole purpose is readability.
2. **Writable CTEs**:  Includes `UPDATE` and `INSERT` constructs. Commonly used to return deleted rows .
3.  **Recursive CTEs**:  The rows returned by the CTE actually varies during the execution of the 
### Standard CTE.
```sql
WITH cty_with_tot_tracts AS (  
	SELECT tract_id, substring(tract_id,1, 5) As county_code, 
	COUNT(*) OVER(PARTITION BY substring(tract_id,1, 5)) As cnt_tracts  
	FROM census.lu_tracts)  
	, cty AS (SELECT MAX(tract_id) As last_tract  
	, county_code, cnt_tracts  
	FROM cty_with_tot_tracts  
	WHERE cnt_tracts < 8  
	GROUP BY county_code, cnt_tracts)  
SELECT cty.last_tract, f.fact_type_id, f.val  
FROM census.facts As f  
INNER JOIN cty ON f.tract_id = cty.last_tract;
```

#### Explanation of above query.
##### 1. Common Table Expressions (CTEs)

The query utilizes Common Table Expressions (CTEs) which are temporary result sets that you can refer to within the main query. CTEs are defined using the `WITH` keyword and make complex queries more readable.

##### CTE: `cty_with_tot_tracts`

```sql

`WITH cty_with_tot_tracts AS (SELECT tract_id, substring(tract_id,1, 5) AS county_code, COUNT(*) OVER(PARTITION BY substring(tract_id,1, 5)) AS cnt_tracts FROM census.lu_tracts)`
```
This CTE is extracting information from the `census.lu_tracts` table. For each `tract_id`, it:

- Retrieves the `tract_id`.
- Extracts the first 5 characters from `tract_id` and labels it as `county_code`.
- Counts the number of tracts for each `county_code` and labels this count as `cnt_tracts`. This count is computed using a window function partitioned by the `county_code`.

##### CTE: `cty`

```sql
, cty AS (SELECT MAX(tract_id) AS last_tract, county_code, cnt_tracts FROM cty_with_tot_tracts WHERE cnt_tracts < 8 GROUP BY county_code, cnt_tracts)`
```
This CTE uses the result from the first CTE, `cty_with_tot_tracts`. It:

- Filters out records where the count of tracts (`cnt_tracts`) is 8 or more.
- For the remaining records, it groups them by `county_code` and `cnt_tracts` and retrieves the maximum `tract_id` for each group, naming it as `last_tract`.

##### 2. Main Query

```sql
`SELECT cty.last_tract, f.fact_type_id, f.val   FROM census.facts AS f   INNER JOIN cty ON f.tract_id = cty.last_tract;`
```

The main query:

- Joins the `census.facts` table (aliased as `f`) with the `cty` CTE based on the `tract_id` from `census.facts` and the `last_tract` from the `cty` CTE.
- Selects the `last_tract`, `fact_type_id`, and `val` from the joined results.

##### In Summary:

The query identifies the tracts in the `census.lu_tracts` table that belong to counties having less than 8 tracts. For such counties, it identifies the tract with the highest `tract_id` value. It then fetches data (`fact_type_id` and `val`) for these specific tracts from the `census.facts` table.


### Writable CTEs:
```sql
t1 AS (DELETE FROM ONLY logs_2011  
WHERE log_ts < '2011-03-01' RETURNING *)  
INSERT INTO logs_2011_01_02 SELECT * FROM t1;
```
The above CTE deletes from logs table and inserts the deleted records into the logs_2011_01_02 table.


## Selective DELETE, UPDATE, and SELECT from Inherited Tables
Selective queries can be run using the only keyword. This prevents postgres from drilling down into the child tables and running the specified query.
## Functions
Function creation syntax is as follows
```sql
CREATE OR REPLACE FUNCTION func_name(arg1 arg1_datatype)  
RETURNS some_type | setof sometype | TABLE (..) AS  
$$  
BODY of function  
$$  
LANGUAGE language_of_function
```

#### Language 
The language installed and the one in which the function is written in.
### Volatility (Stable, Volatile, Immutable)
This setting gives the planner an idea if the results of a function can  
be cached.
**STABLE** means that the function will return the same value for the same  
inputs within the same query. **VOLATILE** means the function may return something  
different with each call, even with same inputs. Functions that change data or are  
a function of other environment settings like time, should be marked as VOLA  
TILE. **IMMUTABLE** means given the same inputs the function is guaranteed to return  
the same result
## Aggregates
Custom aggregates can be created. They can be used in window functions.
## Performance & Optimization.
By using pg_stats, the planner gains a sense of how actual values are dispersed within  
a given column and plan accordingly. The pg_stats table is constantly updated as a  
background process. After a large data load, or a major deletion, you should manually  
update the stats by executing a VACUUM ANALYZE. VACUUM permanently removes deleted  
rows from tables; ANALYZE updates the stats

## IN Operator.
It takes not only an array of values but a query that returns just one column as its return value can be fed into  an IN op.
```sql
select * from cd.facilities where facid in ( select facid from cd.facilities );
```

## HAVING Operator
Used to help with the filtering of output from aggregate functions. This keyword is HAVING.
Postgres, unlike some other RDBMSs like SQL Server and MySQL, doesn't support putting column names in the HAVING clause.

## ROLLUP Operator
In PostgreSQL, the `ROLLUP` is a feature used in combination with the `GROUP BY` clause to generate subtotals and grand totals in the result set, making it easier to create hierarchical or summary reports. It generates multiple levels of grouping with aggregated data, allowing you to see both detailed and summarized information in a single query.

The `ROLLUP` operation produces a result set that includes all the combinations of columns specified in the `GROUP BY` clause, providing subtotals for each combination along with the grand total.

Here's an example to illustrate how `ROLLUP` works:

Let's say you have a sales table with the following columns: `region`, `product`, `quarter`, and `revenue`. You want to create a report that shows the revenue at different levels of aggregation: by region, by region and product, and the grand total.

```sql
SELECT region, product, quarter, SUM(revenue) AS total_revenue
FROM sales
GROUP BY ROLLUP (region, product, quarter);
```

In this query:

- We use `ROLLUP` to specify the columns by which we want to group the data. This generates subtotals for all possible combinations of `region`, `product`, and `quarter`.

The result set will include the following levels of aggregation:

1. Detailed data grouped by `region`, `product`, and `quarter`.
2. Subtotals grouped by `region` and `product`, summing up the revenue for all quarters within each combination.
3. Subtotals grouped by `region` alone, summing up the revenue for all products and quarters within each region.
4. A grand total, summing up the revenue for the entire dataset.

The result set will have rows for each of these levels of aggregation, making it easy to create summary reports with hierarchical data.