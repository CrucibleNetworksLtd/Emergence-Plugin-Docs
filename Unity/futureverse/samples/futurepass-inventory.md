---
title: Futurepass Inventory
description: A demonstration of how to use emergence to Access and Display the inventory of a Futureverse Connected wallet.
parent: Samples
---

# Futurepass Inventory

<figure><img src="../../old-gitbooks-assets/image (62).png" alt=""><figcaption></figcaption></figure>

This demonstrations shows how to utilise the FutureverseInventoryService to display the contents of a Futureverse Inventory in an in game UI. All that's required to do this is an active FV wallet connection (as shown in the Furepass Login demo)

FutureverseInventoryService is a service managed by our EmergenceServiceProvider the service provider dynamically returns the appropriate inventory service when accessed.

```
// Some code
```

Firstly we call the emergence service provider to get the current IInventory service. Because we've connected with the FV login flow this will be the FutreverseInventoryService. As with other functions in the Emergence SDK we can do this using Event binding. here you can see we cache our services as variables within the script.

```csharp
private void Start()
{
    EmergenceServiceProvider.OnServicesLoaded += _ =>
    {
        futureverseService = EmergenceServiceProvider.GetService<IFutureverseService>();
        sessionService = EmergenceServiceProvider.GetService<ISessionService>();
        inventoryService = EmergenceServiceProvider.GetService<IInventoryService>();
    };
    ....
}
```

Now that we've cahced those services we can utilise them to retreive an inventory. We call the InventoryByOwner method on our inventory service.

```csharp
public void ShowInventory()
{
    ...
    
    inventoryService.InventoryByOwner(
        EmergenceServiceProvider.GetService<IWalletService>().WalletAddress,
        InventoryChain.AnyCompatible,
        SuccessInventoryByOwner,
        EmergenceLogger.LogError);
}
```

We pass:\
\- our wallet address\
\- the chain we want to pull NFT's from (in this case any compatible chain)\
\- A callback method to be fired on successful execution\
\- A callback method for error handling.

Our successful callback method will cache all of our inventory items, and then generate some UI elements to represent those items.

```csharp
private void SuccessInventoryByOwner(List<InventoryItem> inventoryItems)
{
    inventoryItemStore.SetItems(inventoryItems); // Cache inventory items
    foreach (var inventoryItem in inventoryItems)
    {
        var entry = CreateEntry();
        entry.GetComponent<InventoryItemEntry>().SetItem(inventoryItem);
    }
}

// Generate a UI element for each inventory item
private GameObject CreateEntry()
{
    return Instantiate(itemEntryPrefab, contentGO.transform, false);
}
```

This dynamically generated inventory will be displayed in scene!
