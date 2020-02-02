---
title: "Suterusu_guide_to_staking_and_minging"
date: 2019-12-18T21:17:19+08:00
---

**Suterusu - Guide to Staking & Mining **

Following the introduction of our blockchain-agnostic, privacy-preserving technology, we [defined](https://medium.com/suterusu/defining-suterusus-staking-and-token-economics-98d220253958) the structure of the Suterusu staking and token economy. In addition, we circumscribed the governance model and its correlation to the native Suter token -- along with detailing the role of validator and nominator nodes.

Now, we want to provide a more detailed guide for staking and mining with Suterusu, and more specifically, the precise distribution of rewards to nominator and validator nodes alluded to in the previous article.

First, it is important to reiterate that the only way to become a nominator node, which verifies transaction data processed by validator nodes, is for users to participate in the private sale. Nominator nodes are then presented with two options at the outset of the network launch:



1. Begin staking strictly as a nominator node
2. Add a validator node and then begin staking as both nominator and validator

_Nominator Nodes, Mortgage-Issuance, & Validator Nodes _

Option 1 is the basic nominator node staking process that we define as analogous to a long-term mortgage contract. Once a user becomes a nominator node via the private sale, their initial Suter token deposit will be locked into a 180-day contract, and is subsequently released through a linear supply schedule within 6 months of the lockout period’s expiration.

Nominators still earn staking rewards, but their deposits will not be released until the expiration of the contract.

The purpose is to encourage active participation by nominator nodes in governance as well as incentivize long-term participation and liquidity of the Suter token.

In total, 76 percent of the 10 billion Suter token cap will be saved explicitly for mining and staking rewards. The deflationary per block supply schedule of Suter tokens will be allocated based on a dynamic community calculation of how to distribute 7.6 billion Suter tokens between the nominator and validator nodes.

The Suter token pool based on the community’s pre-determined parameters. However, that allocation is a function of our proprietary formula for “mining power,” which consists of the following factors:



1. Token Quantity
2. Holding Period
3. Mining Power Index

We expect the precise calculation of the Mining Power Index to crystallize once the private sale is complete, concurrently at the time that validator nodes are ready for the mainnet launch.

At mainnet launch, only nominator nodes will be eligible to run validator nodes (option 2), which will be capped at 100 total and require a minimum deposit of 10 million Suters -- on top of the nominator deposit in the private sale. There are three primary incentives for the nominator nodes to add a validator node:



1. Operating both nominator + validator reduces the lockout period of the nominator deposit.
2. Validator nodes earn a share of mining/staking rewards -- adding to nominator returns.
3. Validator nodes can charge a 10 - 20 percent commission rate from voting community members.

In the first year of the Suterusu network, we can break down the initial reward allocation to hybrid nominator and validator nodes as follows:

_Validator Deposit (10 - 20 million Suters) = 30 percent share of release tokens of nominator node to deposit token of validator node. _

_Validator Deposit (20 - 30 million Suters) = 60 percent share of release tokens of nominator node to deposit token of validator node. _

_Validator Deposit (30+ million Suters) = 300 percent share of release tokens of nominator node to deposit token of validator node. _

To clarify, the reward percentages above are directly linked to the amount of Suter tokens that nodes have staked in the system.

As the early participants to the project, the nominator nodes are also rewarded with Suter tokens, so they can also delegate their token to the validator nodes to maximize their return. This is because the index power of validator nodes is higher than the nominator node.

The additional validator rewards, in conjunction with a diminishing lockout period for nominator deposits, makes the incentive to operate both nodes very appealing for participants in the private sale. Validator nodes can also earn extra Suter tokens within the first 3 months of the network launch by doubling their mining power. The Suter reward pool for the competition will be dispersed on a first-come-first-serve basis.

Eventually, long-term financial incentives will transition to a portion of total transaction fees accrued on the network -- split between validator nodes only.

As we progress further in our development process and complete the private sale, the community governance decisions detailing the calculation of mining power will enable us to provide explicit parameters for Suter returns based on both independent nominator and validator node stakes.

Overall, the staking and mining ecosystem in Suterusu is designed to tether long-term incentives of private sale participants to the network, facilitating a robust network launch and sustainable management of governance procedures.

_Responsibility of validator node_

The validator nodes are required to invest a certain amount of hardware equipment and pay for the maintenance cost to maintain its infrastructure to ensure the security of the Suter network. There are mainly two responsibilities of validators:

1. Transaction validation and mining

2. Participating in the Suter network on-chain governance.

Here are the details of transaction validation for the validation nodes:



1. Invest in hardware in order to join the network and listen for new blocks. When a new block is proposed, validate the block. The block validation of a Suter payment transaction mainly consists of verifying zero-knowledge proof to make sure there is no double-spending attack.
2. The validator nodes are also responsible for assembling new blocks and solving our proof-of-work puzzle to collect the mining reward. Our preliminary choice of PoW hash function will be memory-hard, similar to Ethash used by the Ethereum network. Ethash is ASIC-resistant, which would guarantee the decentralization degree of the Suter network.

In the future, Suter network will adopt a hybrid PoW/PoS system. A random beacon will be applied to select a voter from the stakeholders. The voter will be responsible for generating a signature to approve the blocks mined by the PoW miners. This provides additional checks and balances mechanism on the PoW miners.

The miners are also required to participate in voting whenever there is a necessity for a protocol change. For instance, there will be a transition period from our current PoS governance to hybrid PoW/PoS mechanism. The initial block rewards will goes to the PoW miners and stakeholders according to the amount of contributed mining power. The Suter community will decide how to adjust this proportion by running our community based on-chain governing mechanism in the later development stage.

