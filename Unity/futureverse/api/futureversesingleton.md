---
title: FutureverseSingleton
description: Management Singleton for FV specific behaviours
parent: APIs
grand_parent: Futureverse
---

# FutureverseSingleton

#### Properties

**`int RequestTimeout`**

Gets the timeout in seconds for all requests to Futureverse-owned endpoints.

**`EmergenceEnvironment Environment`**

Gets the current environment. If a forced environment is set, it returns that; otherwise, it returns the default environment.

***

#### Internal Methods

**`IDisposable ForcedEnvironment(EmergenceEnvironment newEnvironment)`**

Forces a different Futureverse environment until disposed. This is a developer feature meant only for testing. It is strongly recommended to use this with the `using` keyword for easiest management.
