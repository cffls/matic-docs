---
id: validator-responsibilities
title: Validator Responsibilties
description: Overview of the responsibilities of being a validator on the Polygon Network
keywords:
  - docs
  - matic
  - polygon
  - validator
  - responsibilities
slug: validator-responsibilities
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

A blockchain validator is someone who is responsible for validating transactions within a blockchain. On the Polygon Network, any participant can be qualified to become a Polygon's validator by running a full node to earn rewards and collect transaction fees. To ensure the good participation by validators, they lock up at least 1 MATIC token as a stake in the ecosystem.

:::info

Currently, there is a limit of 100 active validators at a time. For a detailed description on what a validator is, see [Validator](/docs/maintain/validator/architecture).

:::

## Responsibilities

Any [validator](/docs/maintain/glossary.md#validator) on the Polygon Network has the following responsibilities:

* Technical node operations done by the nodes.
* Operations:
  * Maintain high uptime.
  * Check daily the node related services and processes.
  * Run node monitoring.
  * Keep ETH balance on the signer address.
* Delegation:
  * Be open to delegation.
  * Communicate commission rates.
* Communication:
  * Communicate issues.
  * Provide feedback and suggestions.
* Stake network tokens and run validator nodes to join the system as a validator.
* Earn staking rewards for validating state transitions on the blockchain.

## Technical node operations

The following technical node operations are done automatically by the nodes:

* Block producer selection:
  * Select a subset of validators for the block producer set for each [span](/docs/maintain/glossary.md#span)
  * For each span, select the block producer set again on [Heimdall](/docs/maintain/glossary.md#heimdall) and transmit the selection information to [Bor](/docs/maintain/glossary.md#bor) periodically.
* Validating blocks on Bor:
  * For a set of Bor sidechain blocks, each validator independently reads block data for these blocks and validates the data on Heimdall
* Checkpoint submission:
  * A [proposer](/docs/maintain/glossary.md#proposer) is chosen among the validators for each Heimdall block. The [checkpoint](/docs/maintain/glossary.md#checkpoint-transaction) proposer creates the checkpoint of Bor block data, validates, and broadcasts the signed transaction for other validators to consent to.
  * If >2/3 of the active validators reach consensus on the checkpoint, the checkpoint submitted to the Ethereum mainnet.
* Sync changes to Polygon staking contracts on Ethereum:
  * Continuing from the checkpoint submission step, since this is an external network call, the checkpoint transaction on Ethereum may or may not be confirmed, or may be pending due to Ethereum congestion issues.
  * In this case, there is an `ack/no-ack` process that is followed to ensure that the next checkpoint contains a snapshot of the previous Bor blocks as well. For example, if checkpoint 1 is for Bor blocks 1-256, and it failed for some reason, the next checkpoint 2 will be for Bor blocks 1-512. See also [Heimdall architecture: Checkpoint](/docs/pos/heimdall/checkpoint).
* State sync from the Ethereum mainnet to the Bor sidechain:
  * Contract state can be moved between Ethereum and Polygon, specifically through [Bor](/docs/maintain/glossary.md#bor):
  * A DApp contract on Ethereum calls a function on a special Polygon contract on Ethereum.
  * The corresponding event is relayed to Heimdall and then Bor.
  * A state-sync transaction gets called on a Polygon smart contract and the DApp can get the value on Bor via a function call on Bor itself.
  * A similar mechanism is in place for sending state from Polygon to Ethereum. See also [State Sync Mechanism](/docs/pos/state-sync/state-sync).

## Operations

### Maintain high uptime

A node's uptime on the Polygon network is based on the number of [checkpoint transactions](/docs/maintain/glossary.md#checkpoint-transaction) that the validator node has signed.

Approximately every 34 minutes, a proposer submits a checkpoint transaction to the Ethereum mainnet. The checkpoint transaction must be signed by every [validator](/docs/maintain/glossary.md#validator) on the Polygon network.

Failure to sign a checkpoint transction results in the decrease of your validator node performance.

The process of signing the checkpoint transactions is automated. To ensure your validator node is signing all valid checkpoint transactions, you must maintain and monitor your node health.

### Check daily node services and processes

You must check daily the services and processes associated with [Heimdall](/docs/maintain/glossary.md#heimdall) and [Bor](/docs/maintain/glossary.md#bor).

### Run node monitoring

You must run either:

* Grafana Dashboards provided by Polygon. See GitHub repository: [Matic-Jagar setup](https://github.com/vitwit/matic-jagar).
* Or your own monitoring tools for the [validator](/docs/maintain/glossary.md#validator) and [sentry](/docs/maintain/glossary.md#sentry) nodes.

### Keep an ETH balance

You must maintain an adequate amount of ETH on your validator [signer address](/docs/maintain/glossary.md#signer-address) on the Ethereum mainnet.

You need ETH to:

* Sign the proposed [checkpoint transactions](/docs/maintain/glossary.md#checkpoint-transaction) on the Ethereum mainnet.
* Propose and send checkpoint transactions on the Ethereum mainnet.

Not maintaining an adequate amount of ETH on the signer address will result in:

* Delays in the checkpoint submission. Note that transaction gas prices on the Ethereum network may fluctuate and spike.
* Delays in the finality of transactions included in the checkpoints.
* Delays in subsequent checkpoint transactions.

## Delegation

### Be open for delegation

All validators must be open for delegation from the community.

Each validator has the choice of setting their own commission rate. There is no upper limit to the commission rate.

### Communicate commission rates

It is the moral duty of the validators to communicate the commission rates and the commission rate changes to the community.

The preferred platforms to communicate the commission rates are:

* [Discord](https://discord.com/invite/0xPolygon)
* [Forum](https://forum.polygon.technology/)

## Communication

### Communicate issues

Communicating issues as early as possible ensures that the community and the Polygon team can rectify the problems as soon as possible.

The preferred platforms to communicate the commission rates are:

* [Discord](https://discord.com/invite/0xPolygon)
* [Forum](https://forum.polygon.technology/)
* [GitHub](https://github.com/maticnetwork)

### Provide feedback and suggestions

At Polygon, we value your feedback and suggestions on any aspect of the validator ecosystem.

[Forum](https://forum.polygon.technology/) is the preferred platform to provide feedback and suggestions.
