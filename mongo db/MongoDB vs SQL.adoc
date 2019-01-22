

RDBMS		|	MongoDB	|	Difference
------------|-----------|---------------
Table		|	Collection	|	In RDBMS, the table contains the columns and rows which are used to store the data whereas, in MongoDB, this same structure is known as a collection. The collection contains documents which in turn contains Fields, which in turn are key-value pairs.
Row		|	Document	|	In RDBMS, the row represents a single, implicitly structured data item in a table. In MongoDB, the data is stored in documents.
Column	|	Field	|	In RDBMS, the column denotes a set of data values. These in MongoDB are known as Fields.
Joins	|	Embedded documents	|	In RDBMS, data is sometimes spread across various tables and in order to show a complete view of all data, a join is sometimes formed across tables to get the data. In MongoDB, the data is normally stored in a single collection, but separated by using Embedded documents. So there is no concept of joins in MongoDB.

.

SQL Concepts|	MongoDB 
------------|--------------
Aggregation	|	Operators
WHERE		|	$match
GROUP BY	|	$group
HAVING		|	$match
SELECT		|	$project
ORDER BY	|	$sort
LIMIT		|	$limit
SUM()		|	$sum
COUNT()		|	$sum
join		|	$lookup