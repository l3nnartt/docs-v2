---
title: InfluxDB SQL reference
description: >
  InfluxDB SQL reference
menu:
  influxdb_cloud_iox:
    name: InfluxDB SQL reference
    parent: Query data with SQL
weight: 190
---

InfluxDB Cloud backed by InfluxDB IOx uses the Apache Arrow DataFusion implementation of SQL.  

## Identifiers

An identifier is the name of an object, such as a [`bucket`](/cloud/reference/glossary/#bucket) name (database name), `measurement` name, `tag key`, and `field key`.

## Literals

Literals are the same as constants.  

### String literals

String literals must be surrounded by single quotes. 

```sql
'santa_monica'
'pH'
```

### Number literals

Number literals are positive or negative numbers that are either floats or exact numbers.

```sql
10
+10
-10
10.78654
-100.56
```

### Date and time literals

The following date and time literals are supported:
 - '2022-01-31T06:30:30.123Z' (RFC3339)
 - '2022-01-31T06:30:30.123-8:00' (RFC3339)
 - '2022-01-31 06:30:30.123-8:00' (RFC3339-like)
 - '2022-01-31T06:30:30.123' (RFC3339-like)
 - '2022-01-31 06:30:30.123' (RFC3339-like)
 - '2022-01-31 06:30:30' ((RFC3339-like, no fractional seconds) 
 - 1567296000000000000 (Unix epoch)

All dates and times in RFC3339 and RFC3339 like-format must be in single quotes.  Unix epoch timestamps do not need quotes.  

 ### Boolean literals

Boolean literals are either TRUE or FALSE. 

## Quoting

Rules for quoting:

- Always single quote string literals
- Single quote time durations (excluding Unix epoch) 
- Double quote database identifiers (column names)

The following queries will still both return results:

```sql
SELECT location, water_level 
  FROM h2o_feet

SELECT "location","water_level" 
  FROM "h2o_feet"
```
However, a good rule of thumb is to double quote all database identifiers.

## Duration Units

Duration units specify a length of time.  You must spell out the unit of time.  

```sql
Correct:
interval'400 minutes'

Incorrect:
interval'400m'
```

InfluxDB SQL supports the following duration units:

 - nanoseconds (1 billionth of a second)
 - microseconds (1 millionth of a second)
 - miliseconds (1 thousandth of a second)
 - second
 - minute
 - hour
 - day
 - week 
 - month (verify)
 - year (verify)

| Unit         | Meaning                  |
| :----------- | :----------------------- |
| nanoseconds  | 1 billionth of a second  |
| microseconds | 1 millionth of a second  |
| miliseconds  | 1 thousandth of a second |
| second       |                          |
| minute       |                          |
| hour         |                          |
| day          |                          |
| week         |                          |
| month        |                          |
| year         |                          |

## Arithmetic operators

Arithmetic operators take two numerical values (either literals or variables) and
perform a calculation that returns a single numerical value.

| Operator | Description    | Example  | Result |
|:--------:|:-----------    | -------  | ------ |
| `+`      | Addition       | `2 + 2`  | `4`    |
| `-`      | Subtraction    | `4 - 2`  | `2`    |
| `*`      | Multiplication | `2 * 3`  | `6`    |
| `/`      | Division       | `6 / 3`  | `2`    |

## Comparison operators

Comparison operators compare numbers or strings and perform evaluations.

| Operator | Meaning                  |
|:--------:|:--------                 |
| `=`      | equal to                 |
| `<>`     | not equal to             |
| `!=`     | not equal to             |
| `>`      | greater than             |
| `>=`     | greater than or equal to |
| `<`      | less than                |
| `<=`     | less than or equal to    |

## SQL keywords

| Keyword         | Description                                                                                                                                                                                                                      |
| :-------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AND             | Include columns where all conditions are true                                                                                                                                                                                    |
| AS              | Renames a column with an alias                                                                                                                                                                                                   |
| ASC             | Sorts query results in ascending order                                                                                                                                                                                           |
| DESC            | Sorts query results in descending order                                                                                                                                                                                          |
| DISTINCT        | Selects only distinct values                                                                                                                                                                                                     |
| EXISTS          | Find all rows in a relation where a correlated subquery produces one or more matches for that row. Only correlated subqueries are supported.                                                                                     |
| EXPLAIN         | Shows the logical and physical execution plan for a specified SQL statement                                                                                                                                                      |
| FROM            | Specifies the measurement from which to select data                                                                                                                                                                              |
| GROUP BY        | Groups results by aggregate function                                                                                                                                                                                             |
| HAVING          | Places conditions on results created by the GROUP BY clause                                                                                                                                                                      |
| IN              | Find all rows in a relation where a given expression’s value can be found in the results of a correlated subquery                                                                                                                |
| INNER JOIN      | A join that only returns rows where there is a match in both tables                                                                                                                                                              |
| IS NULL         |                                                                                                                                                                                                                                  |
| IS NOT NULL     |                                                                                                                                                                                                                                  |
| JOIN            | Combines results from two or more tables into one data set                                                                                                                                                                       |
| LEFT JOIN       |                                                                                                                                                                                                                                  |
| LIMIT           | Limits the number of rows in the result.                                                                                                                                                                                         |
| NOT EXISTS      |                                                                                                                                                                                                                                  |
| NOT IN          | Find all rows in a relation where a given expression’s value can not be found in the results of a correlated subquery.                                                                                                           |
| OR              |                                                                                                                                                                                                                                  |
| ORDER BY        | Orders results by the referenced expression                                                                                                                                                                                      |
| FULL OUTER JOIN | A join that is effectively a union of a LEFT OUTER JOIN and RIGHT OUTER JOIN. It will show all rows from the left and right side of the join and will produce null values on either side of the join where there is not a match. |
| RIGHT JOIN      | A join that includes all rows from the right table even if there is not a match in the left table. When there is no match, null values are produced for the left side of the join                                                |
| SELECT          | Retrieves rows from a table (measurement)                                                                                                                                                                                        |
| SELECT DISTINCT | Returns only distinct (different) values                                                                                                                                                                                         |
| UNION           | Used to combine the result set of at least two queries.                                                                                                                                                                          |
| WHERE           | Used o filter results based on fields, tags, and/or timestamps.  |
| WITH            | Names the query and allows for referencing the query by the specified name. |

## Statements and clauses

InfluxDB SQL supports the following basic syntax for queries:

```sql
[ WITH with_query [, …] ]  
SELECT [ ALL | DISTINCT ] select_expr [, …]  
  [ FROM from_item [, …] ]  
  [ JOIN join_item [, …] ]  
  [ WHERE condition ]  
  [ GROUP BY grouping_element [, …] ]  
  [ HAVING condition]  
  [ UNION [ ALL ] ]
  [ ORDER BY expression [ ASC | DESC ][, …] ]  
  [ LIMIT count ]  
```

### The SELECT statement and FROM clause

Use the SQL `SELECT` statement to query data from a specific measurement or measurments. The `FROM` clause always accompanies the `SELECT` statement.  

#### Examples

```sql
SELECT *
FROM "h2o_feet" 

SELECT "location","water_level","time"
FROM "h2o_feet"
```
### The WHERE clause

Use the `WHERE` clause to filter results based on fields, tags, and/or timestamps.

#### Examples

```sql
SELECT * 
FROM "h2o_feet" 
WHERE "water_level"  <= 9

SELECT * 
FROM "h2o_feet" 
WHERE "location" = 'santa_monica' and "level description" = 'below 3 feet' 
```

### The JOIN clause 


### The GROUP BY clause 

Use the `GROUP BY` clause to group query results based on specified tag keys and/or a specified time interval. `GROUP BY` requires an aggregate or selector function in the `SELECT` statement.

#### Examples

```sql
SELECT MEAN("water_level"), "location"
FROM "h2o_feet" 
GROUP BY "location","time"
```

### The HAVING clause

 Use the `HAVING` clause to filter query results based on a spcified condition. The `HAVING` clause must follow the `GROUP BY` clause but precede the `ORDER BY` clause.

#### Examples

```sql

```

### The UNION clause

The `UNION` clause combines the results of two or more SELECT statements without returning any duplicate rows.

#### Examples

```sql
SELECT 'pH'
FROM "h2o_pH"
UNION ALL
SELECT "location"
FROM "h2o_quality"
```
### The ORDER BY clause 

The `ORDER BY` clause orders results by the referenced expression.  The result order is `ASC` **by default**.  You can filter data based on fields, tags, and/or timestamps.

#### Examples

```sql
SELECT "water_level" 
FROM "h2o_feet" 
WHERE "location" = 'coyote_creek'  
ORDER BY time DESC
```

### The LIMIT clause

The `LIMIT` clause limits the number of rows to be a maximum of count rows. The count should be a non-negative integer.

#### Examples

```sql
SELECT "water_level","location" 
FROM "h2o_feet" 
LIMIT 10
```

### The WITH clause 


### The OVER clause 

Used with SQL window functions. 


```sql
SELECT time, water_level 
FROM
(SELECT time, "water_level", row_number() 
 OVER (order by water_level desc) as rn 
FROM h2o_feet) 
WHERE rn <= 3;
```

## Functions

### Aggregates
| Function | Description                           |
| :------- | :------------------------------------ |
| COUNT    | Returns the count of of a column      |
| AVG      | Returns the average value of a column |
| SUM      | Returns the summed value of a column  |
| MEAN     | Returns the mean value of a column    |

#### Examples

```sql

SELECT COUNT("water_level") 
FROM "h2o_feet"

SELECT AVG("water_level"), "location"
FROM "h2o_feet" 
GROUP BY "location"
```

### Selectors

Selector functions are unique to time series databases. They behave like aggregate functions but there are some key differences.

| Function   | Description                                     |
| :--------- | :---------------------------------------------- |
| FIRST      |                                                 |
| LAST       |                                                 |
| MIN        | Returns the smallest value of a selected column |
| MAX        | Returns the smallest value of a largest column  |
| PERCENTILE |                                                 |

### Time series functions

| Function            | Description              |
| :------------------ | :----------------------- |
| time_bucket_gapfill |                          |
| date_bin            |                          |
| date_trunc          |                          |
| date_part           |                          |
| now()               | Returns the current time |
| from_unixtime       |                          |