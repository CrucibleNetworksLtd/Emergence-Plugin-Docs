---
title: GetBlockNumber
parent: EmergenceBlockchainWallet
grand_parent: APIs By Module
layout: default
---

![](GetBlockNumber.png)

Gets the current block number of given chain.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for registering the async method with the GameInstance.|
|UEmergenceChain\*|Blockchain|Blockchain to get the block number of.|

# Outputs

| - | - | - |
|Type|Name|Description|
|int|BlockNumber|The block number of this chain.|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|

# C++
Module: `EmergenceBlockchainWallet`
include: `#include "WalletService/GetBlockNumber.h"`

`UGetBlockNumber::GetBlockNumber()` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnGetBlockNumberCompleted`".

# Additional Information

This class or its parent class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.