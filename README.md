# XATA Subgraph

[XATA](https://xata.fi/) is a decentralized protocol for automated token exchange with built-in MEV protection and gasless transactions.

This subgraph dynamically tracks any pair created by the xata factory. It tracks of the current state of Uniswap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on Xata, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Queries

Below are a few ways to show how to query the xata-subgraph for data. The queries show most of the information that is queryable, but there are many other filtering options that can be used, just check out the [querying api](https://thegraph.com/docs/graphql-api). These queries can be used locally or in The Graph Explorer playground.

## Key Entity Overviews

#### ConveyorV2Factory

Contains data across all of Uniswap V2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### ConveyorV2Pair

Contains data on a specific pair.

#### Transaction

Every transaction on Uniswap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying XATA Data

This query fetches the first 10 swaps.

```graphql
{
  swaps(first:10) {
    id
    pair {
      token0 {
        id
        symbol
        decimals
      }
    }
    amount0In
    amount0Out
    to
  }
}
```
