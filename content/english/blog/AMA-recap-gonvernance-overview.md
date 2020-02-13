---
title: "AMA Recap Governance Overview"
date: 2020-02-12T20:10:00+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
draft: false
---

**

## Q1、Would you please give a brief introduction of yourself and the projects you are working on?

  


Dr. Liu: I currently lead research on token economics and governance system at DFINITY. I am also an Affiliated Economics Professor at Huazhong University of Science and Technology. I specialise in monetary theory, bank supervision, cryptocurrency, token economics and blockchain governance system. I hold a Master of Science in Quantum Computation and a Ph.D. in Economics from ETH Zurich. I was a visiting scholar at the European System of Central Banks and have been invited for talks at major central banks and conferences worldwide.

  
  
  


Dr.Lin: I hold Ph.D. degrees in applied cryptography and privacy-preserving distributed systems from Shanghai Jiao Tong University and the University of Florida, respectively. I worked as a postdoctoral researcher in Swiss Federal Institute of Technology (EPFL), and then as an associate principal engineer in ASTRI, HongKong. I have been working on applied cryptography for more than a decade. I co-founded the Suterusu project and currently serve as the CTO of this project. Yulin is an old friend of mine, and I am very grateful he can be here today despite his busy schedule.&nbsp_place_holder;

Disclaimer: The views expressed in this ama are my own and do not necessarily reflect the official position of the DFINITY Foundation.

## Q2. Why are you interested in working on on-chain governance?

  


First, the blockchain projects need a governance system to coordinate conflicts among participants and to align their incentives with the benign development of the blockchain system.

  


Secondly, the off-chain governance system has attracted criticism of violating the decentralization ethos, as core developers and full-node providers have much more power than ordinary users in the decision making.

  


Compared to the indefinite debates involved in the off-chain governance system, the on-chain governance system has a much quicker turnaround time for decision making.&nbsp_place_holder;

In addition, the on-chain governance system is more transparent in the sense that voting rules are predefined and communicated to the public in advance.&nbsp_place_holder;

The decision making is not controlled or interpreted by centralized entities.&nbsp_place_holder;

Moreover, since voting rules are embedded in the system code, protocol updates are implemented automatically upon ratification, which could largely deter hard forks.

  


## Q3. What are the main categories of blockchain governance？What's the difference between off-chain governance and on-chain governance?

  


The blockchain codebase evolves over time. To update the blockchain codes, various interest groups, e.g. users, core developers and full-node providers (also known as miners in the Bitcoin system), need to reach a consensus on what to keep and what to change. This is not as easy as the interests of these stakeholders are often at odds with each other.&nbsp_place_holder;

  


To tackle these issues, every blockchain project has a governance system to coordinate conflicts among participants and to align their incentives with the benign development of the blockchain system.&nbsp_place_holder;

  


Generally speaking, there are two types of blockchain governance systems: off-chain governance like Bitcoin and Ethereum,&nbsp_place_holder; on-chain governance like DFINITY, tezos and Suterusu.&nbsp_place_holder;

  


The difference lies in whether the voting is conducted and recorded on the blockchain ledger or not.

  
  
  
  


## Q5. We all know that decentralization is important in the blockchain. How to tackle the centralization of voting power?

  


In real-life voting, the plutocrat could manipulate elections by funding their favored candidates/puppets and financing their campaigns. The one-man-one-vote mechanism is susceptible to this money effect. The current political systems designed in the last few centuries have shown feeble and clumsy signs in the presence of newly developed technology. The Cambridge Analytica scandal is a great example to demonstrate the potential of influencing the voting result by targeting social media users. With one-token-one-vote in the blockchain governance system, wealthy users/investors could purchase a large number of tokens and steer the voting towards their favored direction even more easily than the one-man-one-vote system in real life.

  


One way to make the voting power more decentralized is to introduce the flexible lockup period. Users could lock their tokens longer for more voting power. For example, users with 10 tokens locked for 10 months could achieve the same voting power as those (wealthy users) with 100 tokens locked for 1 month. The long lockup period implies that the voter has more skin in the game and thus cares more about the long-run development of the system than those who lock for shorter periods.

  


Another way to make the voting power more decentralized is to replace the one-token-one-vote by the one-account-one-vote. Voters could register voting accounts by filling their government-issued ID information. Registered users have e.g. 10x voting power than the unregistered users. Namely, users could still choose to vote anonymously without registering their accounts. However, voting power is much discounted compared to the registered accounts. The system uses the Zero Knowledge Proof technique to prevent the misuse of users' private data. The voting power increases non-linearly with the number of tokens locked in the account. For example, to acquire one unit of voting power, the voter needs to lock one token in the account. To acquire ten units of voting power, the voter needs to lock more than ten tokens (e.g. 100 tokens for 10 units voting power, i.e. quadratic voting). Such a design reduces the voting power of the wealthy token holders.

  


## Q4. How to gain voting power and preserve vote privacy in on-chain governance?

  


To gain voting power in the governance system, users need to stake their tokens in the system for a certain period. By doing so, voters have skin in the game and thus incentive to vote rationally.&nbsp_place_holder;

  


There are many cryptographic techniques that can preserve vote privacy in "on-chain governance". The homomorphic encryption technique is one of the mainstream approaches. Votes are encrypted so that only voters with private keys could check their own votes. All votes are aggregated and tallied after the voting period. Only the final result is decrypted and revealed to the public.

## Q6. Let's talk about the security issues of the on-chain voting with a focus on privacy. How to resolve privacy issues in electronic voting?

  


Voting on the blockchain falls in the category of electronic voting (i.e. e-voting). Secure e-voting is a well-studied subject in the cryptography literature.

Privacy is one of the most important properties of an e-voting system since a voting system could become vulnerable to corruption and coercion if the adversary can identify how a voter votes. Therefore, a basic e-voting scheme should guarantee its voting privacy and voter anonymity.

  


Many cryptographic primitives have been proposed to resolve the privacy issues in e-voting, such as ring signature, blind signature, threshold homomorphic encryption, and mix-nets, etc. Here is a review of these techniques:

#### Ring signature

One of the most extensively studied anonymous e-voting cryptographic primitives is linkable ring signature. Ring signature was proposed by Rivest, Shamir and Tauman in 2001, and the one-time linkability was later added as an improvement.

Digital signature usually assumes the involved party is identifiable by a public/secret key pair. A ring signature scheme allows any signer hidden in a randomly selected group of people to generate a ring signature without revealing which public key in the ring is responsible for the signature generation. Therefore, it provides anonymity protection for the true signer. However, since the signed message is public, the scheme does not provide vote secrecy.

  


Since a ring signature hides the voter's identity, a voter might try to vote for a particular candidate many times in order to increase the odds of one's favored candidate winning the vote. The one-time linkability property aims to ensure as long as one particular secret key in a ring is used twice, the duplicate signature will be linked and therefore ruled as illegitimate.

  


One-time linkable ring signature can be constructed using a special kind of zero-knowledge proof as shown in, i.e. membership proof. Zero-knowledge proof is a protocol that allows a prover to prove the correctness of a statement without revealing any extra information other than the statement itself. For instance, the zero-knowledge range proof scheme proposed in the Suterusu yellowpaper ([https://github.com/suterusu-team/Suter_yellowpaper](https://github.com/suterusu-team/Suter_yellowpaper)) allows a prover to prove a secret integer belongs to a range, say [0, 1] without revealing which integer it is. In other words, the verifier will be convinced that the secret integer is binary after reading the proof without knowing whether it is 0 or 1.

#### Blind Signature

Another closely-related primitive is a blind signature, which requires a registration phase controlled by a group manager. The voting involves an interaction between the voter and the manager so that the voter can obtain an untraceable blank ballot issued by the manager and cast its vote in encrypted/blinded form.&nbsp_place_holder;

  


However, one needs to use the threshold blind signature scheme to reduce the centralized power of the group manager in the blockchain setting. Note "threshold" here means using threshold cryptography to replace a single group manager with multiple managers so that as long as the majority of them remain honest, both the voter anonymity and vote secrecy can be guaranteed.

Threshold homomorphic encryption

  


An encryption scheme turns a plaintext message into a random string to protect its secrecy. Once a message is encrypted, one has to decrypt the ciphertext before any operation (e.g. summation) can be applied to the underlying messages. However, in some application scenarios, it might not be desirable for the underlying message to be known to those who perform the operation. For instance, the tally clerk only needs to know the sum of the individual votes instead of what each vote is. Homomorphic encryption is a special kind of encryption mechanism that allows anyone with access to the ciphertext of the messages to perform the desired operation homomorphically, meaning the operation over the underlying messages can be performed without decryption.

  


If each voter's vote for a specific candidate or statement is encrypted using homomorphic encryption, the tally clerk will be able to homomorphically generate the encryption of the final vote count without decrypting the ciphertext of each individual vote.

  


Note a malicious voter can increase (or reduce) one's favored candidate (or his opponent)'s chance of winning (or losing) by encrypting a large positive (or negative) number instead of a binary vote. Therefore homomorphic-encryption-based e-voting is usually accompanied with a zero-knowledge range proof, which can prove a secret number is binary without revealing the exact vote. Another challenge is that any entity owning the secret key of the homomorphic encryption scheme will be able to decrypt all the votes. Therefore, a threshold homomorphic decryption mechanism is needed to decentralize the decryption power to a group of entities.

  


#### Mix network

Mix network uses several independent servers to shuffle the input of the encrypted ballots and output the plaintext ballots. However, one has to assume at least one of these mixed servers perform the secret permutation honestly to guarantee voter anonymity.

**  

