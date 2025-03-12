---
title: IChainService
description: Service for interacting with the NFT inventory API.
parent: IEmergenceService
---

# IInventoryService

### Methods

#### `UniTask InventoryByOwner(string address, InventoryChain chain, SuccessInventoryByOwner success, ErrorCallback errorCallback)`

Attempts to get the inventory for the given address. If successful, the `SuccessInventoryByOwner` callback will be called with the inventory.

We currently support the mainnets for: Ethereum, Polygon, Flow, Tezos, Solana and ImmutableX.
