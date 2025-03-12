---
title: EmergenceServiceProvider
description: Class for managing Emergence Services
parent: APIs
grand_parent: Unity Plugin
---

# EmergenceServiceProvider

#### Properties

**`ServiceProfile? LoadedProfile`**

Gets the currently loaded service profile.

#### Events

**`event Action<ServiceProfile> OnServicesLoaded`**

Event triggered when services are loaded.

**`event Action OnServicesUnloaded`**

Event triggered when services are unloaded.

#### Public Methods

**`void Load(ServiceProfile profile)`**

Loads the services based on the specified profile. Triggers the `OnServicesLoaded` event upon completion.

**`T GetService<T>() where T : class, IEmergenceService`**

Gets the service of the specified type. Returns the requested service or `null` if not found.

**`void Unload()`**

Unloads all services and clears the loaded profile. Triggers the `OnServicesUnloaded` event.

