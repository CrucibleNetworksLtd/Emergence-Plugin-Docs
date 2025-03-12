---
title: IFutureverseInventoryService
description: FutureverseInventoryService is responsible for handling inventory-related operations in the Futureverse ecosystem.
parent: APIs
grand_parent: Futureverse
---

# IFutureverseInventoryService

#### Constructor

**`FutureverseInventoryService(IFutureverseService futureverseService)`**

Initializes the `FutureverseInventoryService` with a specified Futureverse service.

#### Public Methods

**`UniTask InventoryByOwner(string address, InventoryChain chain, SuccessInventoryByOwner success, ErrorCallback errorCallback)`**

Inherited from `IInventoryService`. Retrieves the inventory for a given owner address and chain, invoking a success or error callback based on the result.

**`UniTask InventoryByOwnerAndCollection(List<string> collectionIds, SuccessInventoryByOwner success, ErrorCallback errorCallback)`**

Retrieves a list of NFTs owned by the currently connected wallet within the provided collections, invoking a success or error callback based on the result.
