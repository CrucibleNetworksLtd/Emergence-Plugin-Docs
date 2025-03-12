---
title: Getting the Current Persona
parent: Sample Code
---

# Getting the Current Persona

The example provided at the path above demonstrates two different methods for obtaining the current persona in your Unity project using the EmergenceSDK. We will go through the example code and explain the purpose of each section.

For this code to execute properly you must first have logged in using the Emergence overlay.

First, we need to import the necessary namespaces:

```csharp
using EmergenceSDK.Runtime.Internal.Services;
using EmergenceSDK.Runtime.Internal.Types;
using UnityEngine;
```

Next, we define a new class called `GettingCurrentPersona`, which inherits from `MonoBehaviour`. This allows us to attach this script to a GameObject in Unity.

```csharp
class GettingCurrentPersona : MonoBehaviour
{
    private IPersonaService personaService;

    ...
}
```

We declare a private variable `personaService` of type `IPersonaService`, which will be used to access the persona-related services provided by EmergenceSDK.

In the `Awake` method, we initialize the `personaService` variable by getting the `IPersonaService` instance from the `EmergenceServices` class.

```csharp
private void Awake()
{
    personaService = EmergenceServiceProvider.GetService<IPersonaService>();
}
```

The `Start` method is called at the beginning of the script's execution. Here, we call the `GetCurrentPersonaAsync` method to obtain the current persona.

```csharp
private void Start()
{
    GetCurrentPersonaAsync();
}
```

The `GetCurrentPersonaAsync` method is an asynchronous method that waits for the `personaService` to return the current persona. Once the persona is received, it calls the `GetPersonaSuccess` method. If an error occurs, it will call the `ErrorLogger.LogError` method to log the error.

```csharp
private async void GetCurrentPersonaAsync()
{
    await personaService.GetCurrentPersona(GetPersonaSuccess, ErrorLogger.LogError);
}
```

The `GetPersonaSuccess` method is called when the `personaService` successfully returns the current persona.&#x20;

It logs the current persona to the console and calls the `GetCachedPersona` method to get the cached persona.

```csharp
private void GetPersonaSuccess(Persona currentpersona)
{
    Debug.Log($"Found persona: {currentpersona}");
    
    GetCachedPersona();
}
```

The `GetCachedPersona` method gets the cached persona from the `personaService` instance. If a cached persona exists, which it will after using the async method, it logs the cached persona to the console.

```csharp
private void GetCachedPersona()
{
    if (personaService.GetCachedPersona(out Persona persona))
    {
        Debug.Log($"Found cached persona: {persona}");
    }
}
```

You should see your persona logged to the console twice.

Full Code:

```csharp
using EmergenceSDK.Runtime.Internal.Services;
using EmergenceSDK.Runtime.Internal.Types;
using UnityEngine;

namespace EmergenceSDK.Samples.CoreSamples
{
    public class GettingCurrentPersona : MonoBehaviour
    {
        private IPersonaService personaService;

        private void Awake()
        {
            // Initialize the personaService variable by getting the IPersonaService instance from the EmergenceServices class
            personaService = EmergenceServiceProvider.GetService<IPersonaService>();
        }

        private void Start()
        {
            GetCurrentPersonaAsync();
        }

        private async void GetCurrentPersonaAsync()
        {
            // Waits for the personaService to return the current persona and then calls the GetPersonaSuccess method
            await personaService.GetCurrentPersona(GetPersonaSuccess, ErrorLogger.LogError);
        }

        // This method is called when the personaService successfully returns the current persona
        private void GetPersonaSuccess(Persona currentpersona)
        {
            // Logs the current persona to the console
            Debug.Log($"Found persona: {currentpersona}");
            
            // Calls the GetCachedPersona method to get the cached persona
            GetCachedPersona();
        }

        // This method gets the cached persona from the personaService instance
        private void GetCachedPersona()
        {
            // Checks if there is a cached persona and logs it to the console if there is
            if (personaService.GetCachedPersona(out Persona persona))
            {
                Debug.Log($"Found cached persona: {persona}");
            }
        }
    }
}

```
