---
title: "Suterusu Yellow Page Release Explained"
date: 2019-12-19T16:04:42+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
tags: ["Technology"]
---

# Suterusu Yellow Paper Release Explained
We recently released our official yellow paper on our [Github]"https://github.com/suterusu-team", which encompasses the full technical details and specifications of our framework for confidential transactions and our cryptographic modules. The paper irons out our implementation of constant-sized ZK-SNARKs, called ZK-ConSNARKs, as well as our testnet network, confidential payment scheme, and consensus protocols.

Some of the immediate takeaways of the last few years in cryptocurrencies revolve around privacy, scalability, and interoperability. While promising privacy technologies like ZK-SNARKs have broached meaningful developments in crypto network anonymity, significant hurdles remain to guide these networks in line with smart contracts platforms that are tackling scalability and interoperability first.

Fortunately, some recent breakthroughs in zero-knowledge proofs, trusted setups, and more efficient scaling solutions (i.e., PoS consensus) create the potential for a new kind of privacy network -- Suterusu.

We will break down the sections of the yellow paper here for a more cursory look at what the Suterusu Network will entail.

## Testnet Framework

Our testnet is a fork of Substrate, the independent Polkadot testnet analog developed by Parity Technologies.

The Substrate runtime module library is ideal for Suterusu to implement its PoS consensus along with our sophisticated design of the liquid meritocracy. Additionally, WebAssembly enables us to create forkless client updates, provide lightweight capacity, and general interoperability.

Substrate is a valuable means for us to test and smooth the necessary components of our network and is proving highly popular among developers.

## Confidential Payment Scheme

At the core of Suterusu’s anonymity assurances is ZK-ConSNARKs, a constant-sized ZK-SNARK in both computation and communication overhead.

Zero-knowledge proofs provide the most powerful assurances against user unmasking at the blockchain layer, which is why they are ideal for privacy-oriented cryptocurrencies. However, they come with a few drawbacks. Namely, they are costly to produce (computationally), send (communication overhead), and most require a trusted setup -- a ceremony generating the network’s key parameters that has a critical vulnerability.

Efforts to reduce the burdensome nature of crypto transactions with strong privacy assurances (i.e., ZCash’s Sapling) have proved effective, but we plan to take the challenge on head-first.

Our confidential transaction scheme is similar to Zether, which replaces the primary commitment scheme in a UTXO model with Elgamal encryption. We subsequently modify the ZKP scheme accordingly.

Notably, we use our ZKP scheme to prove the correctness of a transaction in a model that does not require a trusted setup. We deploy zero-knowledge range proofs to prevent overflow attacks in confidential payments, and we can further shrink range proofs by removing the prime challenge.

In particular, one of the defining components of Suterusu is the use of ZK-ConSNARKS, which are single non-interactive zero-knowledge arguments with constant sized communication overhead.

These innovations enable Suterusu to be much more secure than many privacy-oriented crypto counterparts, particularly ones that employ ZK-SNARKs. This is important for several reasons, including that privacy becomes more accessible to mainstream users with less computational and bandwidth resources, as well as enables the network to scale with less friction.

Finally, we also lay out the two primary attacks against a Zether chain in the yellow paper:
1. Front-running Attacks
2. Replay Attacks

Both attacks can be protected against by using techniques like proof-of-burn and locking accounts. We will detail more safeguards in the near future.

## Consensus Protocol

Suterusu’s testnet is a hybrid PoW/PoS consensus network. The validators are required to make hardware investments, along with their staking services, to validate and mine transactions. Additionally, validators are responsible for participating in the network’s on-chain governance -- taking the form of a liquid meritocracy.

Block verification by validators primarily consists of verifying the zero-knowledge proof to verify that there were no double-spends on the network. In the context of preventing double spends, trusted setups are also a critical vulnerability where nearly unlimited amounts of tokens could be produced surreptitiously, which is why we opted to remove the trusted setup ceremony.

The specs of our PoW algorithm include the memory-hard algorithm (similar to Ethash) and validator node block assembly.

Future plans include the inclusion of a Random Beacon to randomize the selection of voters from the validator pool. Such voters function as PoW mining analogs. Initial rewards on Suter will be allocated to the hardware-intensive PoW mining of the validators before the transition to the PoS mechanism, which will be set and calibrated by the Suter community.

## Future Work

Now that our yellow paper is released, we look forward to overcoming some challenging tasks down the road. The confidential payment scheme is currently tentative, and we may optimize the protocol to use more practical parameters for our cryptographic modules.

We look forward to the future of Suterusu and our community galvanizing the push towards scalable digital privacy.

