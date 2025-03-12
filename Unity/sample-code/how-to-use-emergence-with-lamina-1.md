---
title: How to use Emergence with Lamina1
parent: Sample Code
---

# How to use Emergence with Lamina1

<iframe src="https://cdn.iframe.ly/sicfTL4xOio" style="aspect-ratio: 1.7; border: 0; width: 100%;" allowfullscreen="" scrolling="no" allow="accelerometer *; clipboard-write *; encrypted-media *; gyroscope *; picture-in-picture *; web-share *;"></iframe>

### Prerequisites

This is a tutorial for integrating the Lamina1 blockchain with Emergence. It assumes you've completed the getting started steps Unity [getting-started.md](../getting-started.md "mention")

### The Emergence Chain Asset

To work with any chain in Emergence you need to use an Emergence chain asset. For Lamina1 there is a chain asset in the resources folder by default.

![](<../old-gitbooks-assets/image (50).png>)

However if you're on an older version you may need to add it manually, to do so create a new chain asset, then input the following details:

**Default Node URL**: [https://rpc-betanet.lamina1.com/ext/bc/C/rpc](https://rpc-betanet.lamina1.com/ext/bc/C/rpc)

**Chain ID**: 7649

**Network Name**: LAMINA1 Betanet

<figure><img src="../old-gitbooks-assets/image (51).png" alt=""><figcaption></figcaption></figure>

### Emergence Configuration

The Emergence prefab in your scene has a field called configuration, attached to that is a configuration asset:

<figure><img src="../old-gitbooks-assets/image (52).png" alt=""><figcaption></figcaption></figure>

The chain field here needs to be replaced with the Lamina1 chain:

<figure><img src="../old-gitbooks-assets/image (53).png" alt=""><figcaption></figcaption></figure>

Once that is all set you are ready to go in terms of using Emergence with Lamina1!

## Smart Contract Example

Let's work through an example using the simple counter smart contract that is included in the sample.

Go to the resources folder in the demo and make a copy of DeployedCounterSmartContract, I've called mine L1-Smart Contract

<figure><img src="../old-gitbooks-assets/image (54).png" alt=""><figcaption></figcaption></figure>

The L1 smart contract object needs to have 2 fields changed:

**Contract Address:** 0xdEff415d7E3e983E93Adcb2Fb113745C0F787bc2

**Chain**: Lamina1Betanet (the L1 chain object)

<figure><img src="../old-gitbooks-assets/image (55).png" alt=""><figcaption></figcaption></figure>

Now lets use these by updating the demo stations in the scene, we need to update the Read and the Write demo stations:

<figure><img src="../old-gitbooks-assets/image (56).png" alt=""><figcaption></figcaption></figure>

The Deployed Contract field in the Read Method and Write Method scripts in the Demostation needs to be updated to use our new smart contract object:

<figure><img src="../old-gitbooks-assets/image (59).png" alt=""><figcaption></figcaption></figure>
