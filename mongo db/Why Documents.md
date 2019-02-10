# Why Documents?
----------------

The document is the natural representation of data. We only broke data up into rows and columns back in the 70s as a way to optimize data access. Back then, storage and compute power was expensive and so it made sense to use developer time to reduce the data set into a schema of rows and column, interlinked by relationships and then normalized between tables to reduce duplication. This process was cost-effective then and so it came to dominate database thinking.

Technology has moved on though and systems are more than capable of managing documents. Documents are, in the form of JSON formatted data, the lingua franca of the Internet and databases like MongoDB have emerged with the ability to naturally understand these documents so they can be efficiently stored, queried and manipulated as documents.

For relational databases, often these objects are created and managed using the subtle smoke and mirrors of ORMs; Object Relational Mappers. They turn the rows and columns, which we carefully disassembled the thing into for the relational database, back into objects, reconstituting their contents. Without an ORM, the application developer writes queries which return data which they can populate an object with. ORMs save the developer a lot of time, but often at the cost of performance versus handcrafted relational queries.

For document databases, there's no breaking up of the data, so there's no need to reconstitute; just retrieve the document and treat it like any other object in your application.
