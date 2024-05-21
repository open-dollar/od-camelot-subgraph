<p align="center">
<img width="60" height="60"  src="https://raw.githubusercontent.com/open-dollar/.github/main/od-logo.svg">
</p>
<h1 align="center">
  OD Subgraph - Camelot
</h1>

Graph Protocol subgraph for Tracking Camelot depositors

## Initial Setup

Run these commands prior to deployment

1. Generate the subgraph's types:

```bash
yarn codegen
```

2. Build the subgraph with the following command:

```bash
yarn build
```

## Initialization commands

The following commands were run to initialize this repo

```bash
graph add 0x00c7f3082833e796A5b3e4Bd59f6642FF44DCD15 --contract-name=nonFungiblePositionManager --abi=abis/nonFungiblePositionManager --merge-entities --start-block=204569401

graph add 0x824959a55907d5350e73e151Ff48DabC5A37a657 --contract-name=nonFungiblePositionManager --abi=abis/nonFungiblePositionManager --merge-entities --start-block=204569401

graph add 0x7647Da336cF43F894aC7A0bf87f04806b2E03bb8 --contract-name=nftPool --abi=abis/nftPool --merge-entities --start-block=204569401

graph add 0xdaE425D131069803Ce2D8E5cfA08356d3eDD125E --contract-name=nitroPool --abi=abis/nitroPool --merge-entities --start-block=204569401
```

## Deploy to Subgraph Studio

1. Create a new subgraph on the hosted service, [Subgraph Studio](https://thegraph.com/studio/)

2. In your newly created subgraph, you'll find instructions for initializing your subgraph with the Graph CLI and
   authenticating with the hosted service. We don't need to initialize the subgraph since we already have the code available to us,
   but we do need to authenticate. To do so, run the following command:

```bash
graph auth --studio SUBGRAPH_SECRET_HERE
```

3. Finally, deploy the subgraph with the following command. Make sure you rename the subgraph name in package.json to match the name of your subgraph:

```bash
yarn deploy
```

## Local Graph node w/ any network

1. Add your RPC endpoint to a ETHEREUM_RPC_URL variable in your .env file. Then, replace the `network` property in `docker-compose.yml` with the following (we'll use Arbitrum-Sepolia as an example):

```yaml
ethereum: "arbitrum-sepolia:${ETHEREUM_RPC_URL}"
```

2. Replace the `network` property in `subgraph.yaml` for each contract with the following (if it's not already arbitrum-sepolia):

```yaml
network: arbitrum-sepolia
```

3. Start the Graph node with the following command. Make sure you wait for the Graph node to start logging its sync progress
   before deploying your subgraph:

```bash
docker-compose up
```

4. Create the subgraph with the following command, making sure to replace the name in package.json with the name of your subgraph:

```bash
yarn create-local
```

5. Deploy the subgraph with the following command, making sure to replace the name in package.json with the name of your subgraph:

```bash
yarn deploy-local
```

6. You can now query the subgraph at http://localhost:8000/subgraphs/name/NAME_OF_YOUR_SUBGRAPH/graphql. It may take a few minutes for the subgraph to sync before you can get results from the query.

## License

Copyright © 2024 OpenFi Foundation, Inc.<br />
This project is MIT licensed.
