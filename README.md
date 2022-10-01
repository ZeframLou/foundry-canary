# Foundry Canary

A minimal foundry repo setup for two purposes:

1) Give examples for doing things that the Foundry docs are not clear about
2) Reproduce Foundry bugs

The examples are put in `examples/`, and the bugs are turned into Github issues.

## Examples

### Deploying and verifying a contract via Foundry script

This example shows how to deploy a contract to one of many desired networks, using Foundry script, and at the same time verifying the contract source on Etherscan (or equivalend block explorer).

#### 1. Set up networks in the Foundry config

It's best practice to list the networks you want to use in the Foundry config like so:

```toml
[rpc_endpoints]
arbitrum = "${RPC_URL_ARBITRUM}"
goerli = "${RPC_URL_GOERLI}"
mainnet = "${RPC_URL_MAINNET}"
optimism = "${RPC_URL_OPTIMISM}"
polygon = "${RPC_URL_POLYGON}"

[etherscan]
arbitrum = {key = "${ARBISCAN_KEY}", url = "https://api.arbiscan.io/api"}
goerli = {key = "${ETHERSCAN_KEY}", url = "https://api-goerli.etherscan.io/api"}
mainnet = {key = "${ETHERSCAN_KEY}"}
optimism = {key = "${OPTIMISM_ETHERSCAN_KEY}", url = "https://api-optimistic.etherscan.io/api"}
polygon = {key = "${POLYGONSCAN_KEY}", url = "https://api.polygonscan.com/api"}
```

#### 2. Set environment variables

The values of the RPC endpoints, Etherscan API keys, and deployer private key should be kept in the `.env` file like so:

```bash
RPC_URL_MAINNET=XXX
RPC_URL_GOERLI=XXX
RPC_URL_ARBITRUM=XXX
RPC_URL_OPTIMISM=XXX
RPC_URL_POLYGON=XXX

PRIVATE_KEY=XXX

ETHERSCAN_KEY=XXX
ARBISCAN_KEY=XXX
POLYGONSCAN_KEY=XXX
OPTIMISM_ETHERSCAN_KEY=XXX
```

of course replacing the XXXs with the actual values.

#### 3. Run deploy script

To deploy to the Goerli testnet for example, run:

```bash
forge script script/Counter.s.sol -f goerli --broadcast --verify
```

this will deploy the `Counter` contract to goerli and verify it at the same time.