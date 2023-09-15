# MongoDB RxStorage (beta)

RxDB MongoDB RxStorage is an RxDB [RxStorage](./rx-storage.md) that allows you to use [MongoDB](https://www.mongodb.com/) as the underlying storage engine for your RxDB database. With this you can take advantage of MongoDB's features and scalability while benefiting from RxDB's real-time data synchronization capabilities.

The storage is made to work with any plain MongoDB Server, [MongoDB Replica Set](https://www.mongodb.com/docs/manual/tutorial/deploy-replica-set/), [Sharded MongoDB Cluster](https://www.mongodb.com/docs/manual/sharding/) or [Atlas Cloud Database](https://www.mongodb.com/atlas/database).


## Limitations of the MongoDB RxStorage
- Multiple node.js servers using the same MongoDB database is currently not supported
- [Attachments](./rx-attachment.md) are currently not supported
- Doing non-RxDB writes on the MongoDB database is not supported. RxDB expects all writes to come from RxDB which update the required metadata. Doing non-RxDB writes can confuse the RxDatabase and lead to undefined behavior.


## Using the MongoDB RxStorage

To use the storage, you simply import the `getRxStorageMongoDB` method and use that when creating the [RxDatabase](./rx-database.md). The `connection` parameter contains the [MongoDB connection string](https://www.mongodb.com/docs/manual/reference/connection-string/).

```ts
import {
    createRxDatabase
} from 'rxdb';
import {
    getRxStorageMongoDB
} from 'rxdb/plugins/storage-mongodb';

const myRxDatabase = await createRxDatabase({
    name: 'exampledb',
    storage: getRxStorageMongoDB({
        connection: 'mongodb://localhost:27017,localhost:27018,localhost:27019'
    })
});
```