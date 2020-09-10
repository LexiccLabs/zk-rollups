# Zk-Rollups

An implementation friendly zk-Rollup for Ethereum.

## What are zk-Rollups

ZK-Rollups are the most active researched solutions for layer 2 constructions. They're capable of increasing scalability
through mass transfer processing rolled into a single transaction.
Where Plasma creates one transaction per transfer, ZK-Rollups bundle hundreds of transfers into a single transaction.
The smart contract will unpack and verify all of the transfers held in a single transaction.

A *zkSNARK* approach is used to present and publicly record the validity of the block on the Ethereum blockchain. SNARKs
reduces computing and storage resources for validating the block by reducing the amount of data held in a transaction.

## Pros and Cons

Pros:

* Reduced fees per user transfer
* Faster than Optimistic Rollup and Plasma
* Blocks will be computed in a parallel computing model which encourages decentralization
* Less data contained in each transaction increases throughput and scalability of layer 2
* Does not require a fraud game verification like Optimistic Rollup, which can delay withdrawals by up to two weeks

Cons:

* The difficulty in computing zero knowledge proof will require data optimization to get maximum throughput
* The initial set up of ZK-Rollups promotes a centralized scheme (see Security Considerations)
* The security scheme assumes a level of unverifiable trust
* Quantum computing poses a threat to hacking the blockchain

## Overview

The ZK-Rollup scheme consists of two types of users:

* Transactors create their transfer and broadcast the transfer to the network. The transfer data consists of an indexed "to" and "from" address, a value to transact, the network fee, and nonce. A shortened 3 byte indexed version of the addresses reduces processing resource needs. The value of the transaction being greater than or less than zero creates a deposit or withdrawal respectively. The smart contract records the data in two Merkle Trees; addresses in one Merkle Tree and transfer amounts in another.

* Relayers collect a large amount of transfers to create a rollup. It is the relayers job to generate the SNARK proof. The SNARK proof is a hash that represents the delta of the blockchain state. State refers to "state of being." SNARK proof compares a snapshot of the blockchain before the transfers to a snapshot of the blockchain after the transfers (i.e. wallet values) and reports only the changes in a verifiable hash to the mainnet.

It is worth noting that anyone can become a relayer so long as they have staked the required bond in the smart contract. This incentivises the relayer not to tamper with or withhold a rollup.

## Security Assumptions

The initial setup of ZK-Rollups is assumed to be a trusted state, when this trust cannot be proven. A small group of developers will be subject matter experts on the initial trusted state. This undermines decentralization and opens the risk of social engineering hacking attacks by convincing a developer to manipulate code or provide vulnerability information.

Quantum computing poses a threat to the ability of being able to crack ZK-Rollups due to the fact that a higher probability exists in being able to "guess" the correct SNARK proof hash than the current encryption protocol.
