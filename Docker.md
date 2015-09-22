##Mongo DB replicaset on same docker container
---

Make sure that you start out by creating the folders on the host that we want the mongo db to map to. You can create them by running the following commands in your home dir

```
$ mkdir mongodata
$ cd mongodata
$ mkdir -p rs0-0 rs0-1 rs0-2
```

Start a docker container with mongo and connect to it interactivily so it won't start the ```mongod``` service by default

```
$ docker run --name rs -ti -v ~/mongodata:/data/db mongo bash
```

Run 3 mongo instances on different ports (eg. 27017, ..18, ..19) by execuring the following commands:

```
$ mongod --port 27017 --fork --logpath=/root/rs0.log --dbpath /data/db/rs0-0 --replSet rs0 --smallfiles --oplogSize 128

$ mongod --port 27018 --fork --logpath=/root/rs1.log --dbpath /data/db/rs0-1 --replSet rs0 --smallfiles --oplogSize 128

$ mongod --port 27019 --fork --logpath=/root/rs2.log --dbpath /data/db/rs0-2 --replSet rs0 --smallfiles --oplogSize 128
```

All mongod instances is now running in a service on the same machine but on different ports. Now, log into the first machine to configure it

```
$ mongo --port 27017
```

Save the following command as a variable ```rsconf``` in the mongo shell.

```
> rsconf = { _id: "rs0", members: [ { _id: 0, host: "localhost:27017" }, { _id: 1, host: "localhost:27018" }, { _id: 2, host: "localhost:27019" } ] }
```

**OBS:** Be sure to replace ```localhost``` with the correct ip of you container.
Next up, run the following command in the mongo shell to initiate to replica set

```
> rs.initiate( rsconf )
> rs.conf()
```

The first command initiates the replica set with your configuration variable (containing the configuration BSON object).

Now run a new docker container and link it to the mongo container created earlier.

```
$ docker run -d --name daemon --link rs:rs -p 37123:37123 lundtoft/skycave:latest bash /root/cave/start-mongo.sh
```

You should now have a SkyCave server connected to a mongo replica set.
