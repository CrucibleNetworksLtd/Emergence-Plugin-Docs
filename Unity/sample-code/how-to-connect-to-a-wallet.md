---
title: How to connect to a Wallet
parent: Sample Code
---

# How to connect to a Wallet

CoreSamples/Scenes/Simple Login Scene.unity \
CoreSamples/Scripts/Examples/SimpleQrLoginScreen.cs

Connecting to a web3 wallet is a crucial step in enabling users to interact with blockchain-based applications. While the EmergenceSDK provides an overlay for handling wallet connections, you might want to bypass the default overlay and integrate the QR code directly into your custom user interface. This example demonstrates how to connect to a web3 wallet using the EmergenceSDK in Unity, giving you more control over the wallet connection process and allowing for a more seamless integration with your application's UI.

The example provided at the path above demonstrates how to connect to a web3 wallet using the EmergenceSDK. The following code communicates with the Emergence LoginManager to detail Login settings and espond to events handled by our Login services This is done using Event Listeners.

First, import the necessary namespaces:

```csharp
using Cysharp.Threading.Tasks;
using EmergenceSDK.Runtime;
using EmergenceSDK.Runtime.Services;
using EmergenceSDK.Runtime.Types;
using TMPro;
using UnityEngine;
using UnityEngine.UI;
```

These namespaces contain various utilities and services that we will need to interact with the EmergenceSDK in Unity.

Next, define a new class called `SimpleQrLoginScreen`, which inherits from `MonoBehaviour`. This allows you to attach this script to a GameObject in Unity.

```csharp
public class SimpleQrLoginScreen : MonoBehaviour
{
    [SerializeField]
    private LoginManager loginManager;
    
    [SerializeField]
    private LoginSettings loginSettings = LoginSettings.Default;
    
    [SerializeField]
    private RawImage qrCodeDisplay; // UI element to display the QR code.

    [SerializeField] private TMP_Text qrCodeText = null;
    
    ...
}
```

Declare four private variables: `loginManager` of type `LoginManager,` `loginSettings` of type `LoginSettings`. This is our Login management singleton and the settings we will use for login flow.

Then Declare some UI elements for displaying your login flow. A RawImage `qrCodeDisplay` and a text element `qrCodeText`. These will serve as visual elements for your Login.

In the `Awake` method, we must first initialise the emergence service provider. This is a class that manages a variety of emergence related services.

```csharp
private void Awake()
{
    // Load the default service provider for the login process.
    EmergenceServiceProvider.Load(ServiceProfile.Default);
    ...
    
```

We then tie a variety of behaviours to various login Events triggered by the login manager. There are a variety of additional methods that can be subscribed to and are demonstrated within the full sample.

```csharp
    ...
    // Set up event listeners for login process steps.
    loginManager.loginStepUpdatedEvent.AddListener(OnLoginStepUpdated);
    loginManager.loginSuccessfulEvent.AddListener(OnLoginSuccessful);
    loginManager.loginCancelledEvent.AddListener(OnLoginCancelled);
    loginManager.qrCodeTickEvent.AddListener(OnQrCodeTick);
    ...
```

We then add a method to launch the login process. we use an asyncronous lambda function to do this. This is to ensure the login manager is ready to begin the login flow before the login starts.

```csharp
    ...
    /// <summary>
    /// Starts the login process for QR-code authentication.
    /// </summary>
    public void StartLogin()
    {
        UniTask.Void(async () =>
        {
            await loginManager.WaitUntilAvailable(); // Ensure LoginManager is ready.
            await loginManager.StartLogin(loginSettings); // Start login with specified settings.
        });
    }
    ...
```

You'll note that we pass our login settings through to the StartLogin method of the LoginManager. These settings dictate the login flow, altering which EmergenceSDK Services are activated and their order of execution. For this sample we'll use the default login settings for a typical Emergence login with handshake.

Now, the login manager will call the events we previously subscribed to:

```csharp
    /// <summary>
    /// Handles updates during the login process.
    /// </summary>
    private void OnLoginStepUpdated(LoginManager _, LoginStep step, StepPhase phase)
    {
        if (phase != StepPhase.Success) return;

        if (step == LoginStep.QrCodeRequest)
        {
            // Display the QR code texture in the assigned UI RawImage.
            Texture2D qrCodeTexture = loginManager.CurrentQrCode.Texture;
            qrCodeTexture.filterMode = FilterMode.Point; // Ensure a crisp QR display.
            qrCodeDisplay.texture = qrCodeTexture;

            Debug.Log("QR code displayed. User can scan to authenticate.");
        }
    }
```

As you can see, when the LoginManager triggers the LoginStepUpdated event it tells it's listeners what its new step is. We want to know when the Loginmanager enters the QrCodeRequest step. This informs us that the LoginManager has sourced a QR code to perform a wallet connection.

We can now present this QR code to the user enabling them to scan on their wallet connect enabled DApp. At this pont the login manager will also begin calling OnQrCodeTick

```csharp
/// <summary>
/// Updates the remaining time for the QR code's validity.
/// </summary>
private void OnQrCodeTick(LoginManager _, EmergenceQrCode qrCode)
{
    qrCodeText.text = ($"QR code expires in: {qrCode.TimeLeftInt} seconds.");
}
```

Here we update QR code text display to inform the user of the QR code's timeout.

Finally, the OnLoginSuccessfulmethod is called when the user responds to the prompts on their DApp, firstly connecting their wallet, and then as part of the Typical emergence login flow, Signs a handshake request.&#x20;

```csharp
/// <summary>
/// Called when the login is successfully completed.
/// </summary>
private void OnLoginSuccessful(LoginManager _, string walletAddress)
{
    LoginManager.SetFirstLoginFlag();
    qrCodeText.text = ($"Login successful. Wallet address: {walletAddress}");
    qrCodeDisplay.gameObject.SetActive(false); // Hide the login screen.
}
```

It receives the wallet address as a parameter. You can now use the wallet address for any necessary operations. The example simply displays this message to the user, but our Emergence SDK session service will retain the wallet information and other emergence services, IE transactions, inventory etc are all able to utilise the connected wallet for their operations.

Now to execute the login flow we simply call the appropriate method on teh login manager, where we pass our "LoginSettings" this flag instructs the login manager which login flow it should execute. By default we'll use wallet connect.

```csharp
    [SerializeField]
    private LoginSettings loginSettings;
    
    private void StartLogin()
    {
        UniTask.Void(async () =>
        {
            await loginManager.WaitUntilAvailable(); // Wait until the login manager is available
            await loginManager.StartLogin(loginSettings); // Start login
        });
    }
```

By following this example, you can connect to a web3 wallet in your Unity project using the EmergenceSDK. Generating a QR code, presenting it to the user for scanning, and completing the handshake to establish a connection with the wallet.



Full Code:

```csharp
using System;
using Cysharp.Threading.Tasks;
using EmergenceSDK.Runtime;
using EmergenceSDK.Runtime.Internal.Services;
using EmergenceSDK.Runtime.Services;
using EmergenceSDK.Runtime.Types;
using TMPro;
using UnityEngine;
using UnityEngine.UI;

namespace EmergenceSDK.Samples.CoreSamples
{
    /// <summary>
    /// A minimalist implementation of a login widget to go with the <see cref="LoginManager"/><para/>
    /// </summary>
    public class SimpleLoginScreen : MonoBehaviour
    {
        [SerializeField]
        private LoginManager loginManager;
        
        [SerializeField]
        private LoginSettings loginSettings;
        
        private void Awake()
        {
            // We need to load a service provider profile
            EmergenceServiceProvider.Load(ServiceProfile.Default);
            
            // Add a listener to the loginStepUpdatedEvent. This is triggered as a log in progresses
            loginManager.loginStepUpdatedEvent.AddListener(OnLoginStepUpdated);
            
            // Handle successful login by simply hiding the gameObject and setting the first-login flag to true
            loginManager.loginSuccessfulEvent.AddListener(OnLoginSuccessful);
            
            loginManager.loginStartedEvent.AddListener(OnLoginStarted);
            loginManager.qrCodeTickEvent.AddListener(OnQrCodeTick);
            loginManager.loginCancelledEvent.AddListener(OnLoginCancelled);
        }

        private void StartLogin()
        {
            UniTask.Void(async () =>
            {
                await loginManager.WaitUntilAvailable(); // Wait until the login manager is available
                await loginManager.StartLogin(loginSettings); // Start login
            });
        }

        private void OnLoginStepUpdated(LoginManager _, LoginStep loginStep, StepPhase stepPhase)
        {
            if (stepPhase != StepPhase.Success) return;

            switch (loginStep)
            {
                case LoginStep.QrCodeRequest: 
                    Texture2D qrCodeTexture2D = loginManager.CurrentQrCode.Texture;
                    //Display QR code to User
                    break;
            }
        }

        private void OnLoginSuccessful(LoginManager _,string walletAddress)
        {
            LoginManager.SetFirstLoginFlag();
            Debug.Log($"Wallet address: {walletAddress}");
        }

        private void OnLoginStarted(LoginManager _)
        {

        }

        private void OnLoginCancelled(LoginManager _)
        {
            
        }

        private void OnQrCodeTick(LoginManager _, EmergenceQrCode qrCode)
        {
            
        }
        
    }
}
```
