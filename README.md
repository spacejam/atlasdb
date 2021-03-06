# AtlasDB
AtlasDB is a transactional layer on top of a key value store.  When designing a
data store to be scalable, transactions are usually the first feature to be
cut.  However they are one of the most useful features for developers.  AtlasDB
allows any key value store that supports durable writes to have transactions.
Once you have transactions, indexes are also easy to add because updates to
rows can just update the indexes and include those writes in a single
transaction.  Provided are KeyValueService implementations of LevelDB and
Cassandra, but any data store worth its salt should make a fine storage layer.

# Consistency
AtlasDB uses classic MVCC and supports Snapshot Isolation and Serializable
Snapshot Isolation.  SI must keep track of the write set in memory to detect
write/write conflicts.  SSI must also keep the read set in memory to detect
read/write conflicts.  This means that write transactions are expected to be
reasonably short lived.  Read-only transactions are allowed to run for longer
and will never conflict with other transactions.

# Schemas
AtlasDB can store keys and values using atlasdb-api directly, but using Schemas can
get you type safely, more readable code and remove a lot of boilerplate
serialization code.  AtlasDB contains a Java DSL to define schemas and a proto
representation that gets stored in the K/V store that can be used by other
tools to inspect the values.  Schema tables can be rendered to Java classes to
easily access tables and keep indexes up to date given the schema.

# Wiki
Make sure to check out the wiki for more details: [https://github.com/palantir/atlasdb/wiki](https://github.com/palantir/atlasdb/wiki)
