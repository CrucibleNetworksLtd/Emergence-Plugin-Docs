---
title: ReadMethodJSONToString
parent: EmergenceBlockchainWallet
ancestor: Unreal Plugin
---

![](ReadMethodJSONToString.PNG)

Returns the ReadMethod's wrapped JSON array as a JSON string. "Return Value" is if it was a success.

# Inputs

| - | - | - |
|Type|Name|Description|
|FJsonObjectWrapper|JSONObject|JSONObject to turn into a string.|

# Outputs

| - | - | - |
|Type|Name|Description|
|bool|Return Value|If it was able to turn it into a string.|
|FString&|OutputString|The returned string.|

# C++
Module: `EmergenceBlockchainWallet`
include: `#include "WalletService/EmergenceJSONHelpers.h"`

`static bool ReadMethodJSONToString(FJsonObjectWrapper JSONObject, FString& OutputString)` - instantiates this method.