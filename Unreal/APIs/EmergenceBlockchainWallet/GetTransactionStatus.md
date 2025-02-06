---
title: GetTransactionStatus
parent: EmergenceBlockchainWallet
grand_parent: APIs By Module
layout: default
---

![](GetTransactionStatus.png)

Gets the status of the transaction.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for registering the async method with the GameInstance.|
|FString|TransactionHash|Hash of the transaction.|
|FString|UEmergenceChain\*|Blockchain to get the transaction status from.|

# Outputs

| - | - | - |
|Type|Name|Description|
|FEmergenceTransaction|Transaction|The details about the transaction.|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|

# C++
Module: `EmergenceBlockchainWallet`
include: `#include "WalletService/GetTransactionStatus.h"`

`UGetTransactionStatus::GetTransactionStatus()` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnGetTransactionStatusCompleted`".

# Additional Information

This class or its parent class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.