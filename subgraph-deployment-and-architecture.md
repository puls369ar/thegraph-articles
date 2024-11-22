# Subgraph Deployment and Architecture
In this guide, we'll create and configure a subgraph, learn it's architecture and deploy it to *TheGraph* node.

First, let's install `graph-cli` using **NPM**
```bash
npm install -g @graphprotocol/graph-cli@latest
```

Before initializing subgraph have *ABI file* of your contract stored in `contractABI.json` file
```bash
graph init --from-contract <TARGET_CONTRACT_ADDRESS> --node https://<TARGET_HOST_DOMAIN>:8030 --network <NETWROK_NAME>
```
Usually 8030 is the port where TheGraph nodes manage indexing processes and where we should deploy subgraph. In another [article](https://github.com/puls369ar/thegraph-articles/blob/main/subgraph-deployment-and-architecture.md) of mine when creating TheGraph node for custom chain, ports together with chain name and RPC URL were set.

You'll be asked to provide some information about the subgraph in the terminal.
* `Protocol` - Etereum if the chain you deploy is EVM compatible
* `Subgraph Slug` - Name your subgraph, I personally prefer `<CONTRACT_NAME>` convention
* `Directory` - Directory name in which whole development environment will be
* `Contract Address` - Will be set by default if you provided it in the command's `--from-contract` argument

Then, graph-cli will unsuccessfully try to fetch `ABI`, `StartBlock`, and `ContractName` one by one. You just reject to repeat the try when tool asks it
```bash
 Do you want to retry? (Y/n)
n
```

and proceed to manually setting this parameters
* `ABI file (path)` - Give `contractABI.json` ABI of the contract path you created earlier
* `Start Block` - This is the number of blocks starting from which emitted events will be indexed by our subgraph, setting the block number of the                    contract's creation is a good practice
* `Contract Name`
* `Index contract events as entities (Y/n)` - Better agree, to make the tool create our env together with already generated *schema, mappings* and                                                other files, otherwise you'll have to structure this all manually which is complex and advanced

The folder named after the subgraph will be generated as a result.

Reserve the place for your subgraph in TheGraph node and deploy it
```
$ graph create --node http://localhost:8020 uniswapv2factory
$ graph deploy uniswapv2factory --ipfs http://localhost:5001 --node http://localhost:8020
```

