# Geo Location Based Search

## Basic System Design and Algorithm
1. At high level we need to store and index each dataset (places, reviews, etc.)
2. To query the massive dataset, the indexing should be read efficient -> real time result is expected

### SQL Solution
- One simple solution could be to store all data in a database like MySQL
- Each place will have its longitude and latitude stored separately in two different columns
- To perform fast search we should have indexes on both of these fields

> Select * from Places where Latitude between X-D and X+D and Longitude betweed Y-D and Y+D

#### Efficiency of the query
- This will work fine if we our dataset rather smaller
- Estimated 500M places to be stored in our service
- Since we have two separate indexes, each index can return huge list performing intersection on which won't be efficient

### Grids
- We can divide the whole map into smaller grids to group locations into smaller sets
- Each grid will store all the places residing within a specific range of Longitude and Latitude
- This will enable us to query only few grids to find nearby places
- Based on given location and radius, we can find all neighboring grids and then query these grids to find nearby places

#### Reasonable Grid Size
- Grid size should not be too large that will contain a lot of places
- Also it should not be too small that there will large number of grids
- Since our grids would be statically defined from fixed grid size, we can easily find the grid number of any location and its neighboring grids
- Now we can quey only few grids to get places of interest

#### Index in memory?
- Maintaining the index in memory will boost the search latency
- key is grid number and value is the list of places contained in that grid

- if radius = 10 miles, area of earth = 200 Square Miles, we have 200M grids => we need 4 bytes number to uniqueyly identify a Grid
- Location ID is 8 bytes
- So we need (4 * 200M) + (8 * 500M) ~= 4 GB memory which can easily fit in modern Servers

#### Problems?
- places are not uniformly distributed. Some grids are densely populated and some are sparsely
- It can be slow for densely populated grids
- It can be sovled if we can dynamically adjust our grid size such that whenever we have grid with a lot of places we break it down to create smaller grids
- Challenges will be:
1. How to identify the grid for given location
2. How to identify neighboring grids

### Dynamic Size Grids
- We start with a grid and go on adding places to it. When a maximum number of places say 500 reaches, we break it down into 4 grids
- Data Structure: A tree in which each node has four children can serve our purpose 
- When a node reaches limit of 500 places, we will break it into 4 child nodes and distribute places among them. So leaf nodes will represent the grids and will hold places
- This tree structure in which each node can have four children is called __QuadTree__

#### How to build a QuadTree?
#### How will we find grid for given location? Tree Traveral -> move on the children with required location. If no children, that is required grid
#### Neighboring Grids? 1. Connect leaf nodes by Doubly Linked list OR 2. Traverse back to parent and find sibliings

#### Memory Requirement for QuadTree?

#### How to insert a new place?
#### What will be the search workflow?

### Data Partitioning