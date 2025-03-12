---
title: IChainService
description: Service for interacting with the chain API.
parent: IEmergenceService
---

# IChainService

#### `UniTask GetTransactionStatus<T>(string transactionHash, string nodeURL, GetTransactionStatusSuccess<T> success, ErrorCallback errorCallback)`

Gets the status of a transaction. If successful, the `GetTransactionStatusSuccess` callback will be called.

#### `UniTask GetHighestBlockNumber<T, U>(string nodeURL, GetBlockNumberSuccess<T> success, ErrorCallback errorCallback)`

Gets the block number of a transaction. If successful, the `GetBlockNumberSuccess` callback will be called.
