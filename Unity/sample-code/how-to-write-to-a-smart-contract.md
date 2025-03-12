---
title: How to write to a smart contract
parent: Sample Code
---

# How to write to a smart contract

Writing to smart contracts is an essential part of interacting with decentralized applications. It allows you to modify the state of the contract by executing transactions and invoking methods that change the data stored on the blockchain. This is useful when you need to store new information, update existing data, or execute specific functions within your application.

The example provided at the path above demonstrates how to write to smart contracts using the EmergenceSDK in Unity. The provided example shows how to create a `ContractInfo` object, and call the `WriteMethod` to execute a smart contract method with the provided input data.

First, import the necessary namespaces:

```csharp
using EmergenceSDK.Runtime.Internal.Utils;
using EmergenceSDK.Runtime.ScriptableObjects;
using EmergenceSDK.Runtime.Services;
using UnityEngine;
```

These namespaces contain various utilities, scriptable objects and services needed to interact with the EmergenceSDK in Unity.

Next, define a new class called `WritingContracts`, which inherits from `MonoBehaviour`. This allows you to attach this script to a GameObject in Unity.

```csharp
public class WritingContracts : MonoBehaviour
{
    [Header("Contract information")]
    // This must be set in the inspector
    public DeployedSmartContract deployedContract;
    // Public string array that is used as input data for the smart contract method
    public string[] body = new string[] { };
    // Public string that is used as input data for the smart contract method
    public string value = "0";

    private IContractService contractService;

    ...
}
```

Declare the following variables:

* `deployedContract`: A public `DeployedSmartContract` variable that must be set in the Unity inspector. There are examples that you can use in the sample project.
* `body`: A public string array that serves as input data for the smart contract method, this will need to change based on the contract chosen.
* `value`: A public string that serves as input data for the smart contract method, this will need to change based on the contract chosen.
* `contractService`: A private `IContractService` variable for interacting with the contract-related services provided by EmergenceSDK.

In the `Awake` method, initialize the `contractService` variable by getting the `IContractService` instance from the `EmergenceServiceProvider` class.

```csharp
public void Awake()
{
    contractService = EmergenceServiceProvider.GetService<IContractService>();
}
```

The `Start` method is called at the beginning of the script's execution. Here, we call the `WriteContract` method to initiate the contract writing process.

```csharp
public void Start()
{
    WriteContract();
}
```

The `WriteContract` method creates ContractInfo using the `deployedContract` variable and calls contractService.WriteMethod once its created. ContractService.WriteMethod takes a callback method to be used upon successful contract write. We'll use OnWriteSuccess for this.

```csharp
public void WriteContract()
{
    // Creates a ContractInfo object with the smart contract address, method name, network name, and default node URL
    var contractInfo = new ContractInfo(deployedContract, "[METHOD NAME]");

    // Calls the ReadMethod method to execute the smart contract method defined in the ABI with an empty input parameter
    contractService.WriteMethod(contractInfo, value, body, OnWriteSuccess, EmergenceLogger.LogError);
}
```

The `OnWriteSuccess` method is called when the `WriteMethod` method executes successfully. It logs the response to the console.

```csharp
private void OnWriteSuccess(BaseResponse<string> response)
{
    // Logs the response to the console
    Debug.Log($"{response}");
}
```

By following this example, you can write to smart contracts in your Unity project using the EmergenceSDK. The process involves creating a `ContractInfo` object, and calling the `WriteMethod` to execute a smart contract method with the provided input data. This allows you to modify the contract's state, store new information, update existing data, or execute specific functions within your application.



Full code:

```csharp
using EmergenceSDK.Runtime.Internal.Utils;
using EmergenceSDK.Runtime.ScriptableObjects;
using EmergenceSDK.Runtime.Services;
using EmergenceSDK.Runtime.Types.Responses;
using UnityEngine;

namespace EmergenceSDK.Samples.CoreSamples.Examples
{
    public class WritingContracts : MonoBehaviour
    {
        [Header("Contract information")]
        // This must be set in the inspector
        public DeployedSmartContract deployedContract;
        // Public string array that is used as input data for the smart contract method
        public string[] body = new string[] { };
        // Public string that is used as input data for the smart contract method
        public string value = "0";

        private IContractService contractService;
        
        public void Awake()
        {
            contractService = EmergenceServiceProvider.GetService<IContractService>();
        }

        public void Start()
        {
            WriteContract();
        }

        // This method is called once the contract is loaded
        private void WriteContract()
        {
            // Creates a ContractInfo object with the smart contract address, method name, network name, and default node URL
            var contractInfo = new ContractInfo(deployedContract, "[METHOD NAME]");

            // Calls the ReadMethod method to execute the smart contract method defined in the ABI with an empty input parameter
            contractService.WriteMethod(contractInfo, value, body, OnWriteSuccess, EmergenceLogger.LogError);
        }

        private void OnWriteSuccess(BaseResponse<string> response)
        {
            // Logs the response to the console
            EmergenceLogger.LogInfo($"{response}");
        }
    }
}
```
