Introduction
========

This is a node.js driver for OrientDB using the OrientDB binary protocol.

Installation
========

```
npm install orientdb
```

As developer you should fork/clone this repo and once you have it on your machine, do the following in your repo directory:

```
npm install
```

Tutorial
========

To start using OrientDB and nodejs, check out the ["Blog Tutorial"](https://github.com/gabipetrovay/node-orientdb/wiki/Blog-Tutorial-with-ExpressJS-and-OrientDB).

Status
========

This OrientDB driver is almost mature now, but we are still testing it. While we use it in production already and therefore it implements a sufficient number of features for making a fully featured application, we recommend you make some thorough tests before you do it as well. If you find any problems, let us know such that we can improve things. Until version 1.0 we also don't guarantee any backwards compatibility and API stability since we are trying things out. But 1.0 should not be far from now.

The following commands are not implemented yet (just pick one and send us a pull request):

* DATACLUSTER_LH_CLUSTER_IS_USED
* DATASEGMENT_ADD
* DATASEGMENT_DROP
* RECORD_CHANGE_IDENTITY
* POSITIONS_HIGHER
* POSITIONS_LOWER
* RECORD_CLEAN_OUT
* POSITIONS_FLOOR
* POSITIONS_CEILING
* CONFIG_GET
* CONFIG_SET
* CONFIG_LIST
* PUSH_RECORD
* PUSH_DISTRIB_CONFIG
* DB_COPY
* REPLICATION
* CLUSTER
* DB_FREEZE
* DB_RELEASE

Supported database versions
========

We test each release against the following OrientDB versions: 1.1.0, 1.3.0.

We've had to drop OrientDB 1.2.0 support because of this [issue](https://github.com/nuvolabase/orientdb/issues/949). If you're using 1.2.0, we strongly encourage you to evaluate 1.3.0.

Testing
========

An OrientDB Graph Edition server instance must be running. Use the [test configuration files](https://github.com/gabipetrovay/node-orientdb/tree/master/config/test) to provide data to the tests about the running instance (user, port, etc.).

Then run:

`npm test`

to run all the tests under `test`, or

`node test/db_open_close.js`

to run a specific test.

And make sure all run before you make a pull request.

NOTE: The `test/z_shutdown.js` will shutdown the server. So make sure it's the last one to run. (i.e. Don't add a test that is after this one in Lexicographical order.)

Connecting to a database
========

```javascript
var orient = require("orientdb"),
    Db = orient.Db,
    Server = orient.Server;

var dbConfig = {
    user_name: "admin",
    user_password: "admin"
};
var serverConfig = {
    host: "localhost",
    port: 2424
};

var server = new Server(serverConfig);
var db = new Db("temp", server, dbConfig);

db.open(function(err) {

    if (err) { console.log(err); return; }

    console.log("Database '" + db.databaseName + "' has " + db.clusters.length + " clusters");
    
}
``` 