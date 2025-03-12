---
title: Sending a Futurepass ARTM
description: This demonstration showcases how to perform ARTM transactions forming asset links between NFTS
parent: Samples
---

# Sending a Futurepass ARTM

<figure><img src="../../old-gitbooks-assets/image (63).png" alt=""><figcaption></figcaption></figure>

SendARTMDemo.cs Demonstrates a sample workflow for performing the CreateLink and DeleteLink Transactions. These are two transactions that alter how two seperate NFT's are "linked" together. To support testing and demonstration we do this using a number of Editor Serialised Variables.

<figure><img src="../../old-gitbooks-assets/image (64).png" alt=""><figcaption></figcaption></figure>

These values represent elements of the ARTM transaction

* Slot: The Link slot on the root NFT to be occupide by the Connecting NFT
* Link A: The root NFT
* Link B: The NFT being linked to the Slot on Link A

First in the strart mission we must create some local references to Emergence Services. Namley the futureverseServie and sessionService

```csharp
private void Start()
{
    EmergenceServiceProvider.OnServicesLoaded += profile =>
    {
        if (profile != ServiceProfile.Futureverse) return;
        futureverseService = EmergenceServiceProvider.GetService<IFutureverseService>();
        sessionService = EmergenceServiceProvider.GetService<ISessionService>();
    };
    ...
}
```

These servies act as our middlemen, consuming our interactions and communicating them to the backend services. Now that we've ensured they're initialised and cached them in our class we can begin our transactions. These transactions happen Asynchronously using Unitask.

```csharp
    /// <summary>
    /// Using the variables we Generate a transaction request which is associated with the currently connected wallet
    /// </summary>
    private async UniTask SendTestArtm()
    {
        EmergenceLogger.LogInfo("Sending ARTM...", true);

        ArtmTransactionResponse artmTransactionResponse;
        try
        {
            if (isFirstTransactionOfSession)
            {
                artmTransactionResponse = await futureverseService.SendArtmAsync(
                "An update is being made to your inventory",
                new List<ArtmOperation>{ new(ArtmOperationType.CreateLink, slot, linkA, linkB) },
                false);
            }
            else
            {
                artmTransactionResponse = await futureverseService.SendArtmAsync(
                "An update is being made to your inventory",
                new List<ArtmOperation>{ new(ArtmOperationType.DeleteLink, slot, linkA, linkB) },
                false);
            }
            ...
        }
    }
```

As you can see, we create a local ArtmTransaction response object and then populate it with the return of our Asyncrhonous ARTM transaction calls performed by the FutureverseService.

Each transaction requires several parameters, this is where the serialised variables we noted earlier come into play. Our transaction parameters are as follows:

* Message: This is the message presented to the user when they are prompt to sign this request in their wallet app
* ArtmOperations: this is a list of operations being performed by this transaction
* Retrieve status: If ture this will call a seperate method that retrieves the transaction status

Lets focus on our create transaction. As part of the asynchronus method call we create a new list of ArtmOperations with a single entry. In this case we mark the Operation Type as "CreateLink", we specify the slot the operation applies to. Then our NFT being linked to where the slot is, and then the NFT being linked to that specific slot. The Delete link operation is much the same but with a different Operation Type

```csharp
artmTransactionResponse = await futureverseService.SendArtmAsync(
"An update is being made to your inventory",
new List<ArtmOperation>{ new(ArtmOperationType.CreateLink, slot, linkA, linkB) },
false);
```

Once we have created our request, we then need to retrieve the status and verify if it was successful or not. We do this by asynchronously calling GetArtmStatusAsync and passing the hash of the transaction we executed.

```csharp
var artmStatusAsync = await futureverseService.GetArtmStatusAsync(artmTransactionResponse.TransactionHash);
EmergenceLogger.LogInfo("ARTM transaction status: " + artmStatusAsync, true);
```

We can then log out the status of our transaction once retrieved!
