---
title: ISessionService
description: Service for interacting with the current Session
parent: IEmergenceService
---

# ISessionService

#### Properties

**`bool IsLoggedIn`**

Indicates whether a full login has been completed. This property is true right before `OnSessionConnected` is called and becomes false right before `OnSessionDisconnected` is called.

**`LoginSettings? CurrentLoginSettings`**

Gets the current login settings for the session. This property is always null when `IsLoggedIn` is false.

**`bool DisconnectInProgress`**

Indicates whether a disconnect operation is in progress. Useful for disabling UI elements during disconnection.

#### Events

**`event Action OnSessionDisconnected`**

Triggered when the session is disconnected. Useful for handling any disconnection-related business logic.

**`event Action OnSessionConnected`**

Triggered when the login flow is completed and the session is connected. Useful for handling any connection-related business logic.

#### Methods

**`bool HasLoginSetting(LoginSettings enableFuturepass)`**

Checks if the specified login setting is enabled.
