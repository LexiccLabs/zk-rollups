# Zk-Rollups

An implementation friendly zk-Rollup for Ethereum.

## What are zk-Rollups


ZK-Rollups are the most active researched solutions for layer 2 constructions. They're capable of increasing scalability 
through mass transfer processing rolled into a single transaction. 
Where Plasma creates one transaction per transfer, ZK-Rollups bundle hundreds of transfers into a single transaction. 
The smart contract will unpack and verify all of the transfers held in a single transaction.

A *zkSNARK* approach is used to present and publicly record the validity of the block on the Ethereum blockchain. SNARKs 
reduces computing and storage resources for validating the block by reducing the amount of data held in a transaction.

## Overview

The ZK-Rollup scheme consists of two types of users: 
  * Transactors create their transfer and broadcast the transfer to the network. The transfer data consists of an indexed "to" and "from" address, a value to transact, the network fee, and nonce. A shortened 3 byte indexed version of the addresses reduces processing resource needs. The value of the transaction being greater than or less than zero creates a deposit or withdrawal respectively. The smart contract records the data in two Merkle Trees; addresses in one Merkle Tree and transfer amounts in another.

  * Relayers collect a large amount of transfers to create a rollup. It is the relayers job to generate the SNARK proof. The SNARK proof is a hash that represents the delta of the blockchain state. State refers to "state of being." SNARK proof compares a snapshot of the blockchain before the transfers to a snapshot of the blockchain after the transfers (i.e. wallet values) and reports only the changes in a verifiable hash to the mainnet.

It is worth noting that anyone can become a relayer so long as they have staked the required bond in the smart contract. This incentivises the relayer not to tamper with or withhold a rollup.

