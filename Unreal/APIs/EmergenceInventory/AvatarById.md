---
title: AvatarById
parent: EmergenceInventory
ancestor: Unreal Plugin
---

![](AvatarById.PNG)

Gets the avatar from a given ID from the Avatar System.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for registering the async method with the GameInstance.|
|FString|AvatarIdString|AvatarIdString of the avatar we want to get the details of.|

# Outputs

| - | - | - |
|Type|Name|Description|
|const FEmergenceAvatarData&|Avatar|This avatar's data.|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|

# C++
Module: `EmergenceInventory`
include: `#include "AvatarService/AvatarById.h"`

`static UAvatarById* UAvatarById::AvatarById(UObject* WorldContextObject, const FString& AvatarIdString)` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnAvatarByIdCompleted`".

# Additional Information

This class or its parent class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.