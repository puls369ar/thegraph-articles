# Graph Node Creation Flow

```bash
graph init --from-contract 0x0BBF792168cC85C6122B29363Ec71aAE84e38100 --node  http://localhost:8030 --network testnet
```

creating a subgraph environment locally
```bash
graph init --from-contract 0x0BBF792168cC85C6122B29363Ec71aAE84e38100 --node  http://localhost:8030 --network testnet
```

spotting a place for subgraph in TheGraph network
```
graph create --node http://localhost:8020 uniswapv2factory
```

running docker node to start a graph node
```
docker run -it   --add-host=host.docker.internal:host-gateway   -e postgres_host=host.docker.internal   -e postgres_port=5432   -e postgres_user=graph-node   -e postgres_pass=password   -e postgres_db=graph-node   -e ipfs=host.docker.internal:5001   -e ethereum=testnet:https://testnet-evm.lif3.com   -p 8000:8000   -p 8020:8020   -p 8030:8030   graphprotocol/graph-node:latest
```
