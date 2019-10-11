# Design Concepts

## Duplicate Data
The Proliferation of Duplicate Videos can have an impact on many levels:
- Data Storage : storage wastes due to multiple copies
- Caching : degraded cache efficiency by taking up space that could be used for unique content
- Network Usage : increased amount of data to be sent over network
- Energy consumption : Higher storage, inefficient cache and network usage could result in energy wastage
- For the end user, these inefficiencies will be realized in the form of duplicate search results, longer video startup times and interrupted streaming.


### Duplication Detection Algorithms:
1. Block Matching
2. Phase Correlation


## Notifier
- health check of servers

## Message/Task Queue = Notifier + Load Balancer + Heart Beat

## File Vs Blob
If you have to store images, how would you save the images?
Blob -> Binary Large Object   (Clob character large object)

Images are typically large in size that we can't save as VARCHAR objects thats why Databases have Blob for large objects.

Databases can guarantee
- Mutability : rows can be  updated column wise
- Transaction
- Indexes
- Access Control

Are we ever going to change the image. If we do it won't pixels, but the whole file. So Mutability is not something we desire.
Transaction property is also not required because we don't do any Atomic operation on image.
Indexes are good for searching. For image file, it is not important.
Access Control is necessary. But same access control can be achieved using file system.

Blob

File
1. Cheaper
2. Faster: because large files are being stored separately
3. Content Delivery Network (CDN) allows fast access

Information about the file will be stored in database, but files will saved in a file system -> Distributed File System.

## Concurrency Control / Transaction Isolation Level
- We can use transactions in SQL databases to avoid any clashes
- If we are using an SQL server we can utilize Transaction Isolation Levels to lock the rows before we can update them
- Increased transaction isolation comes with reduced concurrency -> is accepted as a trade off for the higher transaction isolation levels necessary to maintain database integrity

Transaction Isolation Level are a measure of the extent to which transaction isolation succeeds. It is defined by the presence or absence of the following:
1. __Dirty Reads__ : A dirty read occurs when a transaction reads data that not yet been committed
2. __Nonrepeatable Reads__ : it occurs when a transaction reads the same row twice but gets different data each time
3. __Phantoms__ : A Phantom is a row that matches the search criteria but is not initially seen.