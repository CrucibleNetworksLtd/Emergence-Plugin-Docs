---
title: RequestToSign
parent: EmergenceBlockchainWallet
ancestor: Unreal Plugin
layout: default
---

![](RequestToSign.PNG)

Sends a request to sign a message to the user's WalletConnect'd wallet / Futureverse custodial wallet.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for registering the async method with the GameInstance.|
|const FString&|MessageToSign| The message that they will be presented to sign.|

# Outputs

| - | - | - |
|Type|Name|Description|
|FString|SignedMessage|The signed message, if successful.|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|

# C++
Module: `EmergenceBlockchainWallet`
include: `#include "WalletService/RequestToSign.h"`

`static URequestToSign* RequestToSign(UObject* WorldContextObject, const FString& MessageToSign)` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnRequestToSignCompleted`".

# Additional Information

This class or its parent class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.