# Consistent Hashing
- It is a way of distributing requests among a changing population of web servers. Each slot is then represented by a node in a distributed system.
- **Fault Tolerance** : Consistent hashing has also been used to reduce the impact of **partial system failures** in large web applications as to allow for robust caches without incurring the system wide fallout of a failure. When a server is down, request are silently redirected to working server
- **Load Balancing** : having virtual servers helps to distribute the load in balance way.
- Consistent hashing concept also applies to the design of **DHTs**.

# DHTs with Consistent Hashing
Distributed Hash Table (DHT) is one of the fundamental components used in distributed scalable systems. A hash table needs a key, a value and a hash function where hash function maps the key to a location where value is stored.
### Problem with traditional hashing:
Suppose we are designing a distributed cache with **n** servers and an intuitive hash function would be **k % n**. It is simple and commonly user. But it has two major drawbacks:
1. It is NOT Horizontally Scalable. Whenever a new host is added to the system, all existing mappings are broken and all of them have to be remapped. Maintenance becomes pain where there are huge number of data. Practically it becomes difficult to schedule a downtime to update.
2. It may NOT be Load Balanced, especially for non-uniformly distributed data. Normally, in practice data are not distributed uniformly. For the caching system, it translates into some caches becoming hot and saturated while the others idle and are almost empty.

> In such situations, consistent hashing is good way to improve the caching system.

### What is Consistent Hashing? (DHT Perspective)
- A very useful strategy for distributed caching system and DHTs
- **Efficient Mapping of Keys** : It allows us to distribute data across a cluster in such a way that will **MINIMIZE REORGANIZATION** when nodes are added or removed -> Easy to Scale Up and Scale Down. Only **k/n** keys need to be remapped unlike all **k** keys with simple caching system using mod as hash function.
- Objects are mapped to the same host if possible. When a host if removed, objects on that host are shared by other hosts; when a new host is added, it takes its share from a few hosts without touching other’s share.
