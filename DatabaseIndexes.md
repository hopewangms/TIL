
INDEXING
 
 
 
 
RESOURCES
- DDIA
- Database Internals
- w3schools -- https://www.w3schools.com/sql/sql_create_index.asp
 
 
 
 
 
CONCEPTS
 
- RUM conjecture ("Database Internals" by Alex Petrov)
    Read
    Update
    Memory Overhead
 
- DB = WAL + materialized view
 
 
 
 
 
TYPES of INDICES
 
 
- No index
    - implementations: kafka (which can possibly be thought of as purely a WAL), data warehouses
 
- primary key -- primary key = partition key + (optional) sort key
    - partition key = "what node"
    - sort key = whatever's left for satisfying uniqueness constraint
 
- partitioning strategies
    - hash partitioning (aka "consistent hashing")
    - range partitioning
    - random number trick
 
 
 
- KV-store (hash table)
    - hash partitioning makes a lot of sense here
    - can only be done in RAM, that's why you don't see it in PostgreSQL, etc.
    - implementations: memcached, redis
 
 
- B-tree -- read-optimized
    - implementations: DynamoDB, PostgreSQL
    - variants: Bw-tree, etc. (check out "Database Internals" by Alex Petrov)
- LSM-tree -- write-optimized
    - implementations: Cassandra, Spanner
 
 
 
- secondary indices -- more read optimization
 
 
- local secondary indices
    - this is the "default" / "normal" secondary indices
- global secondary indices
    - probably makes the most sense for read-heavy with key-range queries, and scatter-gather can't be avoided
    - implementations: DynamoDB, possibly Spanner
 
 
 
- multi-dimensional indices
    - concatenated index
    - R-trees
        - implementations: PostgreSQL
    - quad-trees
        - implementations: ElasticSearch
    - geo-hash
        - implementations: redis
 
 
 
- inverted index
    - implementations: ElasticSearch, PostgreSQL, redis
    - example scenarios: text search on a social media site like twitter, google.com, GitHub (recently outgrew ElasticSearch, IIRC)
 
 
- skip list
    - implementations: redis (only)
    - example scenarios: gaming leaderboard
 
 
- vector index
    - implementations: Pinecone, Facebook's Faiss, PlanetScale's MySQL fork, **redis** (wtf)
    - example scenarios: machine learning problems
 
- data cubes & materialized views
    - implementations: data warehouses, databases that support OLAP
 
- count-min sketch
    - in terms of RUM, this is actually very alternative, trading off _accuracy_ for incredible OLAP read latency
    - implementations: Flink, AWS Firehose, Druid, Spark streams, **redis** (wtf) -- "real-time analytics"
 
 
 
