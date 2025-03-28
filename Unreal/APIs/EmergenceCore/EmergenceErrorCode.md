---
title: EmergenceErrorCode
description: These are various BlueprintAutocasts to help you convert between EErrorCodes and other types.
parent: EmergenceCore
ancestor: Unreal Plugin
---

# C++

Module: `EmergenceCore`
include: `#include "Types/EmergenceErrorCode.h"`

## Conv\_IntToErrorCode

In Blueprint, you can create this node by dragging from an `int` variable / output to a `EmergenceErrorCode`, which will automatically add this converter node in the middle.

![](IntToErrorCode.PNG)

```
TEnumAsByte<EErrorCode> UEmergenceErrorCode::Conv_IntToErrorCode(int32 HttpStatus)
```

## Conv\_ErrorCodeToInt

This will convert to `true` if the code is `EmergenceOk`, otherwise will be `false`. Useful for putting after a call to the EVM server to see if code should continue to read the output or whether an error should be handled.
In Blueprint, you can create this node by dragging from an `EmergenceErrorCode` variable / output to an `int`, which will automatically add this converter node in the middle.

![](ErrorCodeToInt.PNG)

```
int32 UEmergenceErrorCode::Conv_ErrorCodeToInt(TEnumAsByte<EErrorCode> ErrorCode)
```

## Conv\_ErrorCodeToBool

In Blueprint, you can create this node by dragging from an `EmergenceErrorCode` variable / output to a `bool`, which will automatically add this converter node in the middle.

![](ErrorCodeToBool.PNG)

```
UEmergenceErrorCode::Conv_ErrorCodeToBool(TEnumAsByte<EErrorCode> ErrorCode);
```
