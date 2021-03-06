```
Directory Structure
	r1
		data
		logs
		mongod.conf
	r2
		data
		logs
		mongod.conf
	r2
		data
		logs
		mongod.conf
```

** mongod.conf**
```
systemLog:
  destination: file
  logAppend: true
  path: E:/Sumit/work/workspaces/MongoDB/replicaset/r1/logs/mongod.log

storage:
  dbPath: E:/Sumit/work/workspaces/MongoDB/replicaset/r1/data
  journal:
    enabled: true

net:
  port: 1000
  bindIp: 127.0.0.1  # Listen to local interface only, comment to listen on all interfaces.

replication:
   replSetName: app1r0
```

```
start "a" mongod --config E:\Sumit\work\workspaces\MongoDB\replicaset\r1\mongod.conf
start "b" mongod --config E:\Sumit\work\workspaces\MongoDB\replicaset\r2\mongod.conf
start "c" mongod --config E:\Sumit\work\workspaces\MongoDB\replicaset\r3\mongod.conf
```
```
mongo --port 1000
```

```
var cfg = {
      _id: "app1r0",
      version: 1,
      members: [
         { _id: 0, host : "localhost:1000" },
         { _id: 1, host : "localhost:2000" },
         { _id: 2, host : "localhost:3000" , "arbiterOnly": true}
      ]
   }
```
```
rs.initiate(cfg)
```