---
title: IPersonaService
description: Service for interacting with the persona API.
parent: IEmergenceService
---

# IPersonaService

#### Properties

**`event PersonaUpdated OnCurrentPersonaUpdated`**

Event fired when the current persona is updated.

#### Methods

**`bool GetCachedPersona(out Persona currentPersona)`**

Attempts to get the current persona from the cache. Returns true if it was found, false otherwise.

**`UniTask GetCurrentPersona(SuccessGetCurrentPersona success, ErrorCallback errorCallback)`**

Attempts to get the current persona from the web service and returns it in the `SuccessGetCurrentPersona` delegate.
