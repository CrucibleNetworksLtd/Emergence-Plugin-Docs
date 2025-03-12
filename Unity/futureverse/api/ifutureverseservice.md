---
title: IFutureverseService
description: The futureverse service is a singular point of entry for most API interaction related to FV. Hosting API root's and various methods for interacting with FV endpoints.
parent: APIs
grand_parent: Futureverse
---

# IFutureverseService

#### Constructor

**`FutureverseService(IWalletService walletService)`**

Initializes the `FutureverseService` with a specified wallet service.

#### Public Methods

**`string GetArApiUrl()`**

Returns the API URL for the Asset Register based on the current environment.

**`string GetFuturepassApiUrl()`**

Returns the API URL for Futurepass based on the current environment.

**`UniTask<ServiceResponse<LinkedFuturepassResponse>> GetLinkedFuturepassAsync()`**

Retrieves the linked Futurepass information.

**`UniTask<ServiceResponse<FuturepassInformationResponse>> GetFuturepassInformationAsync(string futurepass)`**

Retrieves the Futurepass information for a given Futurepass ID.

**`UniTask<List<AssetTreePath>> GetAssetTreeAsync(string tokenId, string collectionId)`**

Retrieves the asset tree for a specified token and collection.

**`UniTask<ArtmStatus> GetArtmStatusAsync(string transactionHash, int initialDelay, int refetchInterval, int maxRetries)`**

Retrieves the status of a transaction, with retry logic.

**`Task<ArtmTransactionResponse> SendArtmAsync(string message, List<ArtmOperation> artmOperations, bool retrieveStatus)`**

Sends an ARTM transaction and optionally retrieves its status.
