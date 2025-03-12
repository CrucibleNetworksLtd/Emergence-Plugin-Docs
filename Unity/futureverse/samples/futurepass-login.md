---
title: Futurepass Login
description: This demonstration shows how to use Emergence to Log in to a Futrepass connected wallet.
parent: Samples
---

# Futurepass Login

<figure><img src="../../old-gitbooks-assets/image (61).png" alt=""><figcaption></figcaption></figure>

For the purposes of this demonstration we use the emergence overlay as our log in interface. To utilise the overlay to perform a FuturePass login we must first update EmergenceSingleton.DefaultLoginFlow to the futrepass login flow.&#x20;

This can be done in two ways:

**Firstly** you may simply update the Serialised Enum on the Emergence Object. Highlighted in red below

<figure><img src="../../old-gitbooks-assets/image (66).png" alt=""><figcaption></figcaption></figure>

Once the default login flow for the overlay has been updated we can then open the Overlay for our typical login flow but now only FuturePass linked wallets may connect.

```csharp
// Open Overlay to display Login process
EmergenceSingleton.Instance.OpenEmergenceUI();
```

When implementing our own login flow as seen in [How to connect to a wallet](../../sample-code/how-to-connect-to-a-wallet.md) we need to pass the appropriate login settings to the login manager when we start the login process to ensure we only accept Futrepass enabled wallets.

```csharp
    [SerializeField]
    private LoginSettings loginSettings = LoginSettings.EnableFuturepass;
    
    private void StartLogin()
    {
        UniTask.Void(async () =>
        {
            await loginManager.WaitUntilAvailable(); // Wait until the login manager is available
            await loginManager.StartLogin(loginSettings); // Start futurepass login
        });
    }
```

