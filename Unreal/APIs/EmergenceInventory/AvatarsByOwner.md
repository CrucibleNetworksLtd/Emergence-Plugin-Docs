---
title: AvatarsByOwner
parent: EmergenceInventory
grand_parent: APIs By Module
layout: default
---

![](AvatarsByOwner.png)

Gets the all the avatars of a given address from the Avatar System.

# Inputs

| - | - | - |
|Type|Name|Description|
|UObject\*|WorldContextObject|The WorldContextObject for this function. This is mainly used for registering the async method with the GameInstance.|
|FString|Address|Address to get the avatars of.|

# Outputs

| - | - | - |
|Type|Name|Description|
|const TArray<FEmergenceAvatarResult>&|Avatars|An array of the avatars associated with this wallet.|
|EErrorCode|StatusCode|Any errors that occured trying to get the data.|

# C++
Module: `EmergenceInventory`
include: `#include "AvatarService/AvatarsByOwner.h"`

`UAvatarsByOwner::AvatarsByOwner()` - instantiates this async method.
`Activate()` - Activates this async method.
In C++, the outputs of the async function can be acted upon by binding to the event delegate "`OnAvatarsByOwnerCompleted`".

# Additional Information

This class or its parent class inherits from `UEmergenceCancelableAsyncBase`, and thefore also has the following functions that can be called on it:

`void Cancel()` - Cancels the requests.

`bool IsActive()` - Checks if the requests are in-flight.