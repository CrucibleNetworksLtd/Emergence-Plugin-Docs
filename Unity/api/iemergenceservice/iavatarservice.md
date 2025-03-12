---
title: IAvatarService
description: Provides access to the avatar API. This service is off chain.
parent: IEmergenceService
---

# IAvatarService

### Methods

#### `UniTask AvatarsByOwner(string address, SuccessAvatars success, ErrorCallback errorCallback)`

Attempts to get the avatars for the given address. If successful, the `SuccessAvatars` callback will be called with the avatars.

#### `UniTask AvatarById(string id, SuccessAvatar success, ErrorCallback errorCallback)`

Attempts to get the avatar for the given ID. If successful, the `SuccessAvatar` callback will be called with the avatar.
