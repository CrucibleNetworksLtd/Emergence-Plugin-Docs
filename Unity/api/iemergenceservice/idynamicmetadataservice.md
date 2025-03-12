---
title: IChainService
description: Gives access to dynamic metadata. This service is off chain.
parent: IEmergenceService
---

# IDynamicMetadataService

### Methods

**`UniTask WriteDynamicMetadata(string network, string contract, string tokenId, string metadata, string authorization, SuccessWriteDynamicMetadata success, ErrorCallback errorCallback)`**

Attempts to write dynamic metadata to the specified contract. There must already be dynamic metadata on the object.

**`UniTask WriteNewDynamicMetadata(string network, string contract, string tokenId, string metadata, string authorization, SuccessWriteDynamicMetadata success, ErrorCallback errorCallback)`**

Attempts to write dynamic metadata to the specified contract. There must not be dynamic metadata on the object.
