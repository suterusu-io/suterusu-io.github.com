---
title: "Why do we need a new client for substrate based blockchain"
date: 2020-02-15T16:47:46+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
draft: false
---
# Why do we need a new client

A zero-knowledge proof is a relatively complicated cryptographic technology. Due to its complexity, it isn’t very easy for most developers and users to use. How to make it easier to let developers use zero-knowledge proof is as important as the algorithm itself. Despite to develop our cryptography algorithm, we feel obligated to provide a more friendly tool to ease the difficulty. To pave the way of easy adoption of zero-knowledge proof is the primary goal we want to achieve through the implementation of our client.
Suterusu project also wants to support blockchains other than based on the substrate; in this case, a more flexible client resides between underlying layer 1 and layer 2 is expected.
Therefore, Suterusu project design and develop their client, released under apache-2 license, which means anyone can fork and build an application on top of it. No matter is for commercial purpose or not. The client is written in OCaml.

# Features of suter_cli

## Ease of use and flexible 
There are several interactions with blockchains full node through RPC calls during a full confidential transaction based on zero-knowledge proof. With suter_cli, we can program the logic required for the transaction, and trigger the batch executions in suter_cli DSL runtime executor. It makes users focus more on business logic rather than the nuance of the underlying implementations.

## Versatility 
There are different schemes of zero-knowledge proof, and their interfaces differ from one to others. The diversity creates significant challenges to users and developers, particularly when people plan to switch from one to anther. They have to develop all the required library each time. Suter_cli creates a general-purpose protocol by leveraging DSL; it makes zero-knowledge proof schemes is agnostic to users and developers. It also helps developers to build application decoupled with base cryptography algorithm and become more agile.

## Security 
The introduction of the DSL interpretation layer makes the application more secure because the user’s operation with zero-knowledge proof are securely checked and logically verified. Suter_cli plans to support form verification in the future.

**More about the syntax and functions of the DSL will be available soon.** 

# Suter_cli architecture and components 
## The architectural diagram as shown in the picture below 
![Architecture](/images/blog/suter_cli.jpg)

## Major components
* Interface Layer 
    * A Suter_cli DSL Scripts Library to support different zkp API, expose JS(generated through Ocaml automatically) and Ocaml API for users to use. 
    * For developers to implement based on suter_cli DSL. 
* DSL Runtime Executor
    * Suter_cli core executor, define and parse DSL syntax.
    * Security audit and DSL command execution. 
* Connection Component
    * Connect and interact with blockchain's node. 

# How to install and test

## Installation 
* Have ocaml environment set up, and make sure it is newer than 4.7.0
* Clone the code and compile it

```
git clone https://github.com/suterusu-team/suter_cli 
cd suter_cli
./configure.sh 
make 
```
* Start substrate node and make it listen on port 9944

```
./wsclient.native -url http://127.0.0.1:9944

```

## Play with it
There are two ways to play with it   
* Interactive mode 

```
> wsclient.native -url http:127.0.0.1

```

After run the command above, you will get a shell like below: from within, you can run command

```
> id := [0]
//An extended json format which can reuse local variables in json fields.
> @send id |> chain_getBlockHash

``` 
Command as above will get the hash value of block 0 of the bloackchain

```
> Response: "0x2895bf7b698e2efaa18eb3a1f0980f983a7778ca74a9abf123e1d08f9789c66b"
```

You may store the value locally for afterwards use. 

```
> hash := @send id |> chain_getBlockHash
```

If you are following so far, it means that you're able to interact with node through API call successfully. 

* Script mode
You may also program all your actions into a script, the default script end with .sbl, ie. chain_getBlockHash.sbl


```
> id := [0]
> @send id |> chain_getBlockHash

```

Then run the command with the scripts as a parameter

```
> wsclient.native -url http:127.0.0.1  chain_getBlockHash.sbl
```





