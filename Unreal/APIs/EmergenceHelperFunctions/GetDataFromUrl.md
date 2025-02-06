---
title: GetDataFromUrl
parent: EmergenceHelperFunctions
ancestor: Unreal Plugin
layout: default
---

![](GetDataFromUrl.png)

Takes a URL string and gets the data. Can be HTTP or IPFS.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for Registering the async method with the GameInstance.|
|const FString&|Url|The Url to get data from. Can be HTTP or IPFS.|

# Outputs

| - | - | - |
|Type|Name|Description|
|const TArray<uint8>&|Data|The bytes returned from this URL.|
|FString|String|The "Content" returned from this URL as a string. Effectively, "HttpResponse->GetContentAsString()".|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|
|bool|Success|If getting data was a success and you should try to process Data or String.|

# C++
Module: `EmergenceHelperFunctions`
include: `#include "GetDataFromUrl.h"`

`UGetDataFromUrl::GetDataFromUrl()` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnGetDataFromUrlCompleted`".

# Additional Information

This class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.