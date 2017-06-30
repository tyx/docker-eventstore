# Event Store Docker Container
**Note: This is not [the official repository](https://github.com/eventStore/eventstore-docker)**

The docker image will be available via the [Docker Hub Event Store Repository]( https://hub.docker.com/r/rezzza/eventstore/)

## Getting Started

Pull the docker image
```
docker pull rezzza/eventstore
```

### Single node run

```
docker run --name eventstore-node -it -p 2113:2113 -p 1113:1113 rezzzza/eventstore
```

### Cluster node run (on docker swarm)

**Note: please don't forget to check you're already in swarm mode.**

Ensure you have `esnet` network: `docker network inspect esnet`. If not you should create it on your swarm manager : `docker network create -d overlay --attachable esnet`

Then to run services on your swarm manager:
```bash
docker service create --replicas 1 --name es1-node --network name=esnet,alias=escluster.net -e EVENTSTORE_CLUSTER_SIZE=3 -e EVENTSTORE_CLUSTER_DNS=escluster.net rezzzza/eventstore
docker service create --replicas 1 --name es2-node --network name=esnet,alias=escluster.net -e EVENTSTORE_CLUSTER_SIZE=3 -e EVENTSTORE_CLUSTER_DNS=escluster.net rezzzza/eventstore
docker service create --replicas 1 --name es3-node --network name=esnet,alias=escluster.net -e EVENTSTORE_CLUSTER_SIZE=3 -e EVENTSTORE_CLUSTER_DNS=escluster.net rezzzza/eventstore
```

More documentation on Event Store's Configuration can be found [here](http://docs.geteventstore.com/server/latest/command-line-arguments)
