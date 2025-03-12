---
title: IChainService
description: Provides access to the contract API.
parent: IEmergenceService
---

# IContractService

### Methods

#### `UniTask ReadMethod<T, U>(ContractInfo contractInfo, U body, ReadMethodSuccess<T> success, ErrorCallback errorCallback)`

Calls a "read" method on the given contract.

#### `UniTask WriteMethod<T, U>(ContractInfo contractInfo, string localAccountName, string gasPrice, string value, U body, WriteMethodSuccess<T> success, ErrorCallback errorCallback)`

Calls a "write" method on the given contract.
