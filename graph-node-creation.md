# Graph Node Creation
This guide shows how to set and configure *TheGraph* node for a custom chain


# Setting Up PostgreSQL and IPFS
Our node uses these two to operate subgraphs and store related metadata. Each of these has it's docker-image that we can set up and run by the following commands


```bash
$ docker run -d --name ipfs -p 5001:5001 ipfs/go-ipfs
$ docker run -d --name postgres --add-host=host.docker.internal:host-gateway -e POSTGRES_USER=graph-node -e POSTGRES_PASSWORD=password -e POSTGRES_DB=graph-node -e POSTGRES_INITDB_ARGS="-E UTF8 --locale=C" -v /path/to/local/postgres/data:/data/postgres -p 5432:5432 postgres
```

Now we have kubo-IPFS (go implementation of IPFS protocol) running on `localhost:5001` port and PostgreSQL with already initialized `graph-node` DB with password named `password` and `locale-C` running on gateway `localhost:5432`. The latest two are crucial for the node to work without problems.

Well let's execute the actual node docker
```bash
$ docker run -it   --add-host=host.docker.internal:host-gateway   -e postgres_host=host.docker.internal   -e postgres_port=5432   -e postgres_user=graph-node   -e postgres_pass=password   -e postgres_db=graph-node   -e ipfs=host.docker.internal:5001   -e ethereum=customChain:<CHAIN_RPC_URL>   -p 8000:8000   -p 8020:8020   -p 8030:8030   graphprotocol/graph-node:latest
```
Please make sure you are using a gateway host and be careful to pass the right port for IPFS and PostgreSQL, for the latest also pass the right *DB name* and *password*. The argument where chain RPC and Network Name are given `-e ethereum=customChain:<CHAIN_RPC_URL>` is important. We'll use this name later when deploying subgraphs.


If everything is fine then you should see a confirming response message on `localhost:8000` and be able to deploy subgraphs using `localhost:8030` port. Checkout the [article](https://github.com/puls369ar/thegraph-articles/blob/main/subgraph-deployment-and-architecture.md) explaining how to do that and other related articles present in the repo too. 
