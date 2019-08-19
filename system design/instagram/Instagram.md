# Instagram or Flickr or Picasa

Instagram is a social networking service which enables its users to upload and share their photos and videos with other users.

### Requirements

#### Functional Requirements

- Upload/download/view photos.
- Searches based on photo/video titles.
- Users can follow other users.
- News Feed consisting of top photos from all the people the user follows.

### Capacity planning
##### Image Storage


- Let’s assume we have 500M total users, with 1M daily active users.
- 2M new photos every day, 23 new photos every second.
- Average photo file size => 200KB
- Total space required for 1 day of photos: 2M * 200KB => 400 GB
- Total space required for 10 years: 400GB * 365 (days a year) * 10 (years) ~= 1425TB

##### Database storage
We need to store data about users, their uploaded photos, and people they follow. Photo table will store all data related to a photo; we need to have an index on (PhotoID, CreationDate) since we need to fetch recent photos first.

Let’s estimate how much data will be going into each table and how much total storage we will need for 10 years.

- User: Assume 500 million users. Assuming each “int” and “dateTime” is four bytes, each row in the User’s table will be of 68 bytes: 

(UserID (4 bytes) + Name (20 bytes) + Email (32 bytes) + DateOfBirth (4 bytes) + CreationDate (4 bytes) + LastLogin (4 bytes)) * Number of users = 68 bytes * 500 million ~= 32GB

- Photo: Each row in Photo’s table will be of 284 bytes: 

(PhotoID (4 bytes) + UserID (4 bytes) + PhotoPath (256 bytes) + PhotoLatitude (4 bytes) + PhotLongitude(4 bytes) + UserLatitude (4 bytes) + UserLongitude (4 bytes) + CreationDate (4 bytes)) * Number of photos per day = 284 bytes  * 2M ~= 0.5GB per day

If 2M new photos get uploaded every day, we will need 0.5GB of storage for one day:

For 10 years we will need 1.88TB of storage.

- UserFollow: Each row in the UserFollow table will consist of 8 bytes. If we have 500 million users and on average each user follows 500 users. We would need 1.82TB of storage for the UserFollow table:

500 million users * 500 followers * 8 bytes ~= 1.82TB

Total space required for all tables for 10 years will be 3.7TB:

32GB + 1.88TB + 1.82TB ~= 3.7TB

### Architecure
![System design](architecture.png)

### Choosing database and storage
- We can store photos in a distributed file storage like HDFS or S3.
- We can store the metadata and photo id in a distributed key-value store to enjoy the benefits offered by NoSQL. All the metadata related to photos can go to a table where the ‘key’ would be the ‘PhotoID’ and the ‘value’ would be an object containing PhotoLocation, UserLocation, CreationTimestamp, etc.
- We need to store relationships between users and photos, to know who owns which photo. We also need to store the list of people a user follows. For both of these tables, we can use a wide-column datastore like Cassandra. For the ‘UserPhoto’ table, the ‘key’ would be ‘UserID’ and the ‘value’ would be the list of ‘PhotoIDs’ the user owns, stored in different columns. We will have a similar scheme for the 'UserFollow'.


### Reliability and Redundancy
![System design](image-redundancy.png)

### Ranking and News Feed Generation
What are the different approaches for sending News Feed contents to the users?

- Pull: Clients can pull the News Feed contents from the server on a regular basis or manually whenever they need it. Possible problems with this approach are a) New data might not be shown to the users until clients issue a pull request b) Most of the time pull requests will result in an empty response if there is no new data.

- Push: Servers can push new data to the users as soon as it is available. To efficiently manage this, users have to maintain a Long Poll request with the server for receiving the updates. A possible problem with this approach is, a user who follows a lot of people or a celebrity user who has millions of followers; in this case, the server has to push updates quite frequently.

- Hybrid: We can adopt a hybrid approach. We can move all the users who have a high number of follows to a pull-based model and only push data to those users who have a few hundred (or thousand) follows. Another approach could be that the server pushes updates to all the users not more than a certain frequency, letting users with a lot of follows/updates to regularly pull data.

### Cache
Our service would need a massive-scale photo delivery system to serve the globally distributed users. Our service should push its content closer to the user using a large number of geographically distributed photo cache servers and use CDNs.

We can introduce a cache for metadata servers to cache hot database rows. We can use Memcache to cache the data and Application servers before hitting database can quickly check if the cache has desired rows. Least Recently Used (LRU) can be a reasonable cache eviction policy for our system. Under this policy, we discard the least recently viewed row first.

How can we build more intelligent cache? If we go with 80-20 rule, i.e., 20% of daily read volume for photos is generating 80% of traffic which means that certain photos are so popular that the majority of people read them. This dictates that we can try caching 20% of daily read volume of photos and metadata.

### Main tools and technologies
- Amazon CloudFront as the CDN.
- PostgreSQL (users, photo metadata, tags, etc)
- Several terabytes of photos are stored on Amazon S3.
- Redis powers their main feed, activity feed, sessions system, and other services.
- Apache Solr powers the geo-search API.
- 6 memcached instances for caching.


## References:

- https://www.educative.io/collection/page/5668639101419520/5649050225344512/5673385510043648

- http://highscalability.com/blog/2011/12/6/instagram-architecture-14-million-users-terabytes-of-photos.html

- https://www.puncsky.com/hacking-the-software-engineer-interview/#cracking-the-system-design-interview-designing-pinterest-or-instagram-as-an-example
