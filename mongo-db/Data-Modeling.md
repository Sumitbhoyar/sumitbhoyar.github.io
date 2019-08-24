# Data Modeling


### Model One-to-One Relationships with Embedded Documents
    {
       _id: "joe",
       name: "Joe Bookreader",
       address: {
                  street: "123 Fake Street",
                  city: "Faketon",
                  state: "MA",
                  zip: "12345"
                }
    }

### Model One-to-Many Relationships with Embedded Documents

    {
       _id: "joe",
       name: "Joe Bookreader",
       addresses: [
                    {
                      street: "123 Fake Street",
                      city: "Faketon",
                      state: "MA",
                      zip: "12345"
                    },
                    {
                      street: "1 Some Other Street",
                      city: "Boston",
                      state: "MA",
                      zip: "12345"
                    }
                  ]
     }
### Model One-to-Many Relationships with Document References

    {
       _id: "oreilly",
       name: "O'Reilly Media",
       founded: 1980,
       location: "CA"
    }
    
    {
       _id: 123456789,
       title: "MongoDB: The Definitive Guide",
       author: [ "Kristina Chodorow", "Mike Dirolf" ],
       published_date: ISODate("2010-09-24"),
       pages: 216,
       language: "English",
       publisher_id: "oreilly"
    }
    
    {
       _id: 234567890,
       title: "50 Tips and Tricks for MongoDB Developer",
       author: "Kristina Chodorow",
       published_date: ISODate("2011-05-06"),
       pages: 68,
       language: "English",
       publisher_id: "oreilly"
    }

## Model tree structure

### Child References

    db.categories.insert( { _id: "MongoDB", children: [] } )
    db.categories.insert( { _id: "dbm", children: [] } )
    db.categories.insert( { _id: "Databases", children: [ "MongoDB", "dbm" ] } )
    db.categories.insert( { _id: "Languages", children: [] } )
    db.categories.insert( { _id: "Programming", children: [ "Databases", "Languages" ] } )
    db.categories.insert( { _id: "Books", children: [ "Programming" ] } )

The query to retrieve the immediate children of a node

    db.categories.findOne( { _id: "Databases" } ).children
### Parent References

    db.categories.insert( { _id: "MongoDB", parent: "Databases" } )
    db.categories.insert( { _id: "dbm", parent: "Databases" } )
    db.categories.insert( { _id: "Databases", parent: "Programming" } )
    db.categories.insert( { _id: "Languages", parent: "Programming" } )
    db.categories.insert( { _id: "Programming", parent: "Books" } )
    db.categories.insert( { _id: "Books", parent: null } )

The query to retrieve the parent of a node

    db.categories.findOne( { _id: "MongoDB" } ).parent
### Array of Ancestors

    db.categories.insert( { _id: "MongoDB", ancestors: [ "Books", "Programming", "Databases" ], parent: "Databases" } )
    db.categories.insert( { _id: "dbm", ancestors: [ "Books", "Programming", "Databases" ], parent: "Databases" } )
    db.categories.insert( { _id: "Databases", ancestors: [ "Books", "Programming" ], parent: "Programming" } )
    db.categories.insert( { _id: "Languages", ancestors: [ "Books", "Programming" ], parent: "Programming" } )
    db.categories.insert( { _id: "Programming", ancestors: [ "Books" ], parent: "Books" } )
    db.categories.insert( { _id: "Books", ancestors: [ ], parent: null } )

The query to retrieve the ancestors or path of a node

    db.categories.findOne( { _id: "MongoDB" } ).ancestors

## Database References
MongoDB applications use one of two methods for relating documents:

-   Manual references  where you save the  `_id`  field of one document in another document as a reference. Then your application can run a second query to return the related data. These references are simple and sufficient for most use cases.
    
-   DBRefs are references from one document to another using the value of the first document’s  `_id`  field, collection name, and, optionally, its database name. By including these names, DBRefs allow documents located in multiple collections to be more easily linked with documents from a single collection.
    
    To resolve DBRefs, your application must perform additional queries to return the referenced documents. Many  drivers have helper methods that form the query for the DBRef automatically. The drivers do not  _automatically_ resolve DBRefs into documents.

Unless you have a compelling reason to use DBRefs, use manual references instead.
For nearly every case where you want to store a relationship between two documents, use manual references . The references are simple to create and your application can resolve references as needed.

The only limitation of manual linking is that these references do not convey the database and collection names. If you have documents in a single collection that relate to documents in more than one collection, you may need to consider using DBRefs.