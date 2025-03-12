---
title: FutureverseSingleton
description: A management script that is attached to the Emergence object. It provides configuration options for Futureverse API Calls.
parent: Futureverse
---

# FutureverseSingleton

<figure><img src="../old-gitbooks-assets/image (60).png" alt=""><figcaption></figcaption></figure>

Located on the Third Party Game object it allows developers to configure FV API interaction Behaviour

* Request Timeout: The timeout counter in seconds for FV API Requests.
* Environment: This is used to determine the code environment for Futureverse services. This will alter the Base URLs for FV Web Requests. These are shown below

API URL

```csharp
EmergenceEnvironment.Production => "https://ar-api.futureverse.app/graphql",
EmergenceEnvironment.Development => "https://ar-api.futureverse.dev/graphql",
EmergenceEnvironment.Staging => "https://ar-api.futureverse.cloud/graphql",
```

Indexer URL

```csharp
EmergenceEnvironment.Production => "https://account-indexer.api.futurepass.futureverse.app/api/v1/",
EmergenceEnvironment.Development => "https://account-indexer.api.futurepass.futureverse.dev/api/v1/",
EmergenceEnvironment.Staging => "https://account-indexer.api.futurepass.futureverse.dev/api/v1/",
```
