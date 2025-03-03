---
title: How to read / write to smart contracts
parent: Unreal Examples
layout: default
---

# How to read / write to smart contracts


Check out the tutorial below for a tutorial of reading and writing to smart contracts.
<iframe src="https://www.youtube.com/embed/thcO1Mx5AP8" style="aspect-ratio: 1.7; border: 0; width: 100%;" allowfullscreen="" scrolling="no" allow="accelerometer *; clipboard-write *; encrypted-media *; gyroscope *; picture-in-picture *; web-share *;"></iframe>

An example of this can be found in the Emergence Sample Project, check it out [here](https://github.com/CrucibleNetworksLtd/EmergenceSDKUnreal/releases)!

To read or write to a smart contract, you'll first need to set up the relevant [deployed contract asset](./Unreal/AssetTypes), or use the [CreateEmergenceDeployment function](./Unreal/APIs/EmergenceCore/CreateEmergenceDeployment) as an input to either [ReadMethod](/Unreal/APIs/EmergenceBlockchainWallet/ReadMethod) or [WriteMethod](/Unreal/APIs/EmergenceBlockchainWallet/WriteMethod).

 If a method mutates the data on the blockchain, its a "write" method. If it returns data, its a "read" method. When interacting with a smart contact that has functions with parameters, you must send the correct amount of parameters for the function you're talking to in the parameters array.
 
 Additionally, keep in mind that WriteMethod requires the player to be already logged in with WalletConnect, or Futureverse web login flow (for clients), or the write method must be sent with a private key (intended for game servers). 

