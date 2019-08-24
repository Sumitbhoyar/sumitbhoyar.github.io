# Column Store Databases

As the name suggests, wide-column stores use columns to store data. You can group related columns into column families. Individual rows then constitute a column family.

**Schema**: Keyspace

**Table**: Column Families

- A column family consists of multiple rows.
- Each row can contain a different number of columns to the other rows. And the columns don’t have to match the columns in the other rows (i.e. they can have different column names, data types, etc).
- Each column is contained to its row. It doesn’t span all rows like in a relational database. Each column contains a name/value pair, along with a timestamp. Note that this example uses Unix/Epoch time for the timestamp.

A typical column family contains a row key as the first column, which uniquely identifies that row within the column family. The following columns then contain a column key, which uniquely identifies that column within the row, so that you can query their corresponding column values.

Here’s a breakdown of each element in the row:

- **Row Key**: Each row has a unique key, which is a unique identifier for that row.
- **Column**: Each column contains a name, a value, and timestamp.
- **Name**: This is the name of the name/value pair.
- **Value**: This is the value of the name/value pair.
- **Timestamp**: This provides the date and time that the data was inserted. This can be used to determine the most recent version of data.

### Benefits of Column Store Databases

- **Compression**. Column stores are very efficient at data compression and/or partitioning.
- **Aggregation queries**. Due to their structure, columnar databases perform particularly well with aggregation queries (such as SUM, COUNT, AVG, etc).
- **Scalability**. Columnar databases are very scalable. They are well suited to massively parallel processing (MPP), which involves having data spread across a large cluster of machines – often thousands of machines.
- **Fast to load and query**. Columnar stores can be loaded extremely fast. A billion row table could be loaded within a few seconds. You can start querying and analysing almost immediately.

### Examples of Column Store DBMSs
- Bigtable
- Cassandra
- HBase
- Vertica

### Use cases
- **Spotify** uses Cassandra to store user profile attributes and metadata about artists, songs, etc. for better personalization
- **Facebook** initially built its revamped Messages on top of HBase, but is now also used for other Facebook services like the Nearby Friends feature and search indexing
- Sensor Logs  (Internet of Things -IOT)
- User preferences
- Geographic information
- Reporting systems
- Time Series Data
- Logging and other write heavy applications



