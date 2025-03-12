---
title: How to connect to a Futurepass enabled wallet
parent: How-Tos
ancestor: Futureverse
---

# How to connect to a Futurepass enabled wallet.

Samples/FutureverseSamples/Scenes/Simple Futureverse Login Scene.unity \
Samples/FutureverseSamples/Scripts/SimpleQrLoginScreen.cs

Connecting to a Web3 wallet using Futurepass login in the EmergenceSDK enables developers to provide both **QR code-based** and **custodial** login options for futurepass interaction. This guide demonstrates how to integrate these two login methods into your Unity project, bypassing the default overlay for a more custom user interface. Furthermore this sample also demonstrates how to utilise the LoginSettings to avoid Activation of Emergence Specific services, Like Personas.

The example provided at the path above is a fully built demonstration of how to connect to a Futurepass enabled wallet using the EmergenceSDK. The following code communicates with the Emergence LoginManager to detail Login settings and espond to events handled by our Login services This is done using Event Listeners.

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

Next, define a new class called `FutureverseLoginSample`, which inherits from `MonoBehaviour`. This allows you to attach the script to a GameObject in Unity.

```csharp
public class FutureverseLoginSample : MonoBehaviour
{
    [SerializeField]
    private LoginManager loginManager;

    [SerializeField] 
    private GameObject buttonsPanel; // Panel containing login buttons.

    [Header("QR Code Login")]
    [SerializeField]
    private LoginSettings qrLoginSettings = LoginSettings.EnableFuturepass | LoginSettings.DisableEmergenceAccessToken;

    [SerializeField]
    private Button qrLoginButton; // Button to start QR login.

    [SerializeField] 
    private GameObject qrCodePanel; // Panel for QR code UI.

    [SerializeField]
    private RawImage qrCodeImage; // Displays the QR code.

    [SerializeField]
    private TMP_Text qrCodeMessageText; // QR code status message.

    [Header("Custodial Web Login")]
    [SerializeField]
    private LoginSettings custodialWebLoginSettings = LoginSettings.EnableCustodialLogin | LoginSettings.EnableFuturepass | LoginSettings.DisableEmergenceAccessToken;

    [SerializeField]
    private Button custodialWebLoginButton; // Button to start custodial login.

    [SerializeField] 
    private GameObject custodialWebLoginPanel; // Panel for custodial login UI.

    [SerializeField]
    private TMP_Text custodialWebLoginMessageText; // Custodial login status message.

    private bool isQrCodeLogin = false;
}

```

This class declares several private fields:

* **`loginManager`**: The login manager handles the login flow.
* **`qrLoginSettings` and `custodialWebLoginSettings`**: These `LoginSettings` fields configure the respective login methods, using `DisableEmergenceAccessToken` to remove Emergence-specific authentication steps. IE  auth with Personas service
* **UI Elements**: Buttons, panels, and text elements for controlling and displaying the login flows.

In the `Awake` method, we must first initialise the emergence service provider. This is a class that manages a variety of emergence related services. We pass it a profile that specifies that we want all services related to Futureverse to be activated!

```csharp
private void Awake()
{
    // Load the default service provider for the login process.
    EmergenceServiceProvider.Load(ServiceProfile.Futureverse);
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

We then add methods to launch the respective login processes.&#x20;

**QR Code Login**

The `StartQrCodeLogin` method starts the QR login flow by hiding the buttons panel and displaying the QR code UI. It uses an asynchronous lambda to ensure the login manager is ready before proceeding.

```csharp
    ...
    /// <summary>
    /// Starts the login process for QR-code authentication.
    /// </summary>
    private void StartQrCodeLogin()
    {
        isQrCodeLogin = true;
        buttonsPanel.SetActive(false);
        qrCodePanel.SetActive(true);
    
        UniTask.Void(async () =>
        {
            await loginManager.WaitUntilAvailable(); // Ensure LoginManager is ready.
            await loginManager.StartLogin(qrLoginSettings); // Start QR login.
        });
    }
    ...
```

You'll note that we pass our login settings through to the StartLogin method of the LoginManager. These settings dictate the login flow, altering which EmergenceSDK Services are activated and their order of execution. The sample included in the package uses: DisableEmergenceAccessToken and Enable Futurepass. This wil prevent the activation of some emergence specific services, IE Personas, Whilst enabling Futurepass logins.

**Custodial Login**

The `StartCustodialLogin` method initiates the custodial login flow, instructing users to complete authentication in their browser.

```csharp
private void StartCustodialLogin()
{
    isQrCodeLogin = false;
    buttonsPanel.SetActive(false);
    custodialWebLoginPanel.SetActive(true);
    custodialWebLoginMessageText.text = "Please follow instructions in your default browser for authentication...";

    UniTask.Void(async () =>
    {
        await loginManager.WaitUntilAvailable(); // Ensure LoginManager is ready.
        await loginManager.StartLogin(custodialWebLoginSettings); // Start custodial login.
    });
}

```

Once again we pass loginSettings, In this case they are: DisableEmergenceAccessToken, Enable Futurepass and EnableCustodialLogin. This disables emergence specific services, enables futurepass, and enables the custodial login handling.

Now, the login manager will call the events we previously subscribed to:

```csharp
        /// <summary>
        /// Handles updates during the login process.
        /// </summary>
        private void OnLoginStepUpdated(LoginManager _, LoginStep step, StepPhase phase)
        {
            if (phase != StepPhase.Success) return;

            switch (step)
            {
                case LoginStep.QrCodeRequest:
                    // Update the QR code display.
                    Texture2D qrCodeTexture = loginManager.CurrentQrCode.Texture;
                    qrCodeTexture.filterMode = FilterMode.Point; // Crisp rendering.
                    qrCodeImage.texture = qrCodeTexture;

                    Debug.Log("QR code displayed. User can scan to authenticate.");
                    break;

                case LoginStep.CustodialRequests:
                    custodialWebLoginMessageText.text = "Custodial login in progress...";
                    Debug.Log("Custodial login in progress...");
                    break;
            }
        }
```

The `OnLoginStepUpdated` method listens for updates during the login process. For the QR code flow, it displays the QR code texture. For custodial login, it provides a success message once authentication begins.

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

Finally, the OnLoginSuccessfulmethod is called when the user either responds to the prompts on their DApp, connecting their futrepase Enabled wallet, OR, successfully navigates the Custodial Web Login Flow displayed in their browser.

```csharp
/// <summary>
/// Called when the login is successfully completed.
/// </summary>
private void OnLoginSuccessful(LoginManager _, string walletAddress)
{
    LoginManager.SetFirstLoginFlag();
    if (isQrCodeLogin)
    {
        qrCodeImage.gameObject.SetActive(false);
        qrCodeMessageText.text = $"Login successful. Wallet address: {walletAddress}";
    }
    else
    {
        custodialWebLoginMessageText.text = $"Login successful. Wallet address: {walletAddress}";
    }
}
```

It receives the wallet address as a parameter. You can now use the wallet address for any necessary operations. The example simply displays this message to the user, but our Emergence SDK session service will retain the wallet information and other emergence services, IE transactions, inventory etc are all able to utilise the connected wallet for their operations.



By following this example, you can connect to a web3 wallet in your Unity project using the EmergenceSDK. Generating a QR code, presenting it to the user for scanning, and completing the handshake to establish a connection with the wallet.



Full Code:

```csharp
using Cysharp.Threading.Tasks;
using EmergenceSDK.Runtime;
using EmergenceSDK.Runtime.Services;
using EmergenceSDK.Runtime.Types;
using TMPro;
using UnityEngine;
using UnityEngine.UI;

namespace EmergenceSDK.Samples.FutureverseSamples
{
    /// <summary>
    /// A sample login implementation showcasing both Futureverse QR-code and custodial logins.
    /// </summary>
    public class FutureverseLoginSample : MonoBehaviour
    {
        [SerializeField]
        private LoginManager loginManager;

        [SerializeField] 
        private GameObject buttonsPanel;
        
        [Header("QR Code Login")]
        // The DisableEmergenceAccessToken login setting will remove the Emergence specific authentication from the login flow.
        [SerializeField]
        private LoginSettings qrLoginSettings = LoginSettings.EnableFuturepass | LoginSettings.DisableEmergenceAccessToken; 
        
        [SerializeField]
        private Button qrLoginButton; // Button to start QR login.

        [SerializeField] 
        private GameObject qrCodePanel; // Container for QR code UI
        
        [SerializeField]
        private RawImage qrCodeImage; // UI element for QR code.

        [SerializeField]
        private TMP_Text qrCodeMessageText; // UI element for custodial login messages.
        
        [Header("Custodial Web Login")]
        [SerializeField]
        private LoginSettings custodialWebLoginSettings = LoginSettings.EnableCustodialLogin | LoginSettings.EnableFuturepass | LoginSettings.DisableEmergenceAccessToken;
        
        [SerializeField]
        private Button custodialWebLoginButton; // Button to start custodial login.
        
        [SerializeField] 
        private GameObject custodialWebLoginPanel; // Container for CustodialWebLogin UI
                
        [SerializeField]
        private TMP_Text custodialWebLoginMessageText; // UI element for custodial login messages.

        private bool isQrCodeLogin = false;
        

        private void Awake()
        {
            // Load the Futureverse service provider. This enables all teh relevant Emergence Services
            EmergenceServiceProvider.Load(ServiceProfile.Futureverse);

            // Set up event listeners.
            loginManager.loginStepUpdatedEvent.AddListener(OnLoginStepUpdated);
            loginManager.loginSuccessfulEvent.AddListener(OnLoginSuccessful);
            loginManager.loginCancelledEvent.AddListener(OnLoginCancelled);
            loginManager.qrCodeTickEvent.AddListener(OnQrCodeTick);

            // Bind button actions.
            qrLoginButton.onClick.AddListener(StartQrCodeLogin);
            custodialWebLoginButton.onClick.AddListener(StartCustodialLogin);
        }

        /// <summary>
        /// Starts the QR-code login process.
        /// </summary>
        private void StartQrCodeLogin()
        {
            isQrCodeLogin = true;
            buttonsPanel.SetActive(false);
            qrCodePanel.SetActive(true);
            UniTask.Void(async () =>
            {
                await loginManager.WaitUntilAvailable(); // Ensure the LoginManager is ready.
                await loginManager.StartLogin(qrLoginSettings); // Start the Futureverse QR login.
            });
        }

        /// <summary>
        /// Starts the custodial login process.
        /// </summary>
        private void StartCustodialLogin()
        {
            isQrCodeLogin = false;
            buttonsPanel.SetActive(false);
            custodialWebLoginPanel.SetActive(true);
            custodialWebLoginMessageText.text = "Please follow instructions in your default browser for authentication...";
            UniTask.Void(async () =>
            {
                await loginManager.WaitUntilAvailable(); // Ensure the LoginManager is ready.
                await loginManager.StartLogin(custodialWebLoginSettings); // Start custodial login.
            });
        }

        /// <summary>
        /// Handles updates during the login process.
        /// </summary>
        private void OnLoginStepUpdated(LoginManager _, LoginStep step, StepPhase phase)
        {
            if (phase != StepPhase.Success) return;

            switch (step)
            {
                case LoginStep.QrCodeRequest:
                    // Update the QR code display.
                    Texture2D qrCodeTexture = loginManager.CurrentQrCode.Texture;
                    qrCodeTexture.filterMode = FilterMode.Point; // Crisp rendering.
                    qrCodeImage.texture = qrCodeTexture;

                    Debug.Log("QR code displayed. User can scan to authenticate.");
                    break;

                case LoginStep.CustodialRequests:
                    custodialWebLoginMessageText.text = "Custodial login in progress...";
                    Debug.Log("Custodial login in progress...");
                    break;
            }
        }

        /// <summary>
        /// Called when the login process is successfully completed.
        /// </summary>
        private void OnLoginSuccessful(LoginManager _, string walletAddress)
        {
            LoginManager.SetFirstLoginFlag();
            if (isQrCodeLogin)
            {
                qrCodeImage.gameObject.SetActive(false);
                qrCodeMessageText.text =($"Login successful. Wallet address: {walletAddress}");
            }
            else
            {
                custodialWebLoginMessageText.text =($"Login successful. Wallet address: {walletAddress}");
            }
        }

        /// <summary>
        /// Called if the login process is cancelled.
        /// </summary>
        private void OnLoginCancelled(LoginManager _)
        {
            Debug.LogWarning("Login process was cancelled.");
            custodialWebLoginMessageText.text = "Login cancelled. Please try again.";
        }

        /// <summary>
        /// Updates the remaining time for the QR code's validity.
        /// </summary>
        private void OnQrCodeTick(LoginManager _, EmergenceQrCode qrCode)
        {
            qrCodeMessageText.text = $"QR code expires in: {qrCode.TimeLeftInt} seconds.";
        }
    }
}

```

