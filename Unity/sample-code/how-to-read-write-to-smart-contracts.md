---
title: How to read and write to smart contracts
parent: Sample Code
---

# How to read smart contracts

In decentralized applications, you often need to interact with smart contracts to perform various operations, such as querying data or executing transactions. Reading smart contracts allows you to obtain information stored on the blockchain without modifying the contract's state. This is particularly useful when you need to display the data in your application or make decisions based on the contract's current state.

The example provided at the path above demonstrates how to read smart contracts using the EmergenceSDK in Unity. The example provided shows how to create a `ContractInfo` object, and call the `ReadMethod` to execute a smart contract method.

First, import the necessary namespaces:

```csharp
using EmergenceSDK.Runtime.Internal.Utils;
using EmergenceSDK.Runtime.ScriptableObjects;
using EmergenceSDK.Runtime.Services;
using UnityEngine;
```

These namespaces contain various utilities, scriptable objects and services needed to interact with the EmergenceSDK in Unity.

Next, define a new class called `ReadingContracts`, which inherits from `MonoBehaviour`. This allows you to attach this script to a GameObject in Unity.

```csharp
public class ReadingContracts : MonoBehaviour
{
    // This must be set in the inspector
    public DeployedSmartContract deployedContract;
    
    // Public string array that is used as input data for the smart contract method
    public string[] data = new string[] { "1" };

    private IContractService contractService;

    ...
}
```

Declare the following variables:

* `deployedContract`: A public `DeployedSmartContract` variable that must be set in the Unity inspector. There are examples that you can use in the sample project.
* `data`: A public string array that serves as input data for the smart contract method, this will need to change based on the contract chosen.
* `contractService`: A private `IContractService` variable for interacting with the contract-related services provided by EmergenceSDK.

In the `Awake` method, initialize the `contractService` variable by getting the `IContractService` instance from the `EmergenceServiceProvider` class.

```csharp
public void Awake()
{
    contractService = EmergenceServiceProvider.GetService<IContractService>();
}
```

The `Start` method is called at the beginning of the script's execution. Here, we call the `ReadContract` method to initiate the contract reading process.

```csharp
public void Start()
{
    ReadContract();
}
```

The `ReadContract` method creates ContractInfo using the `deployedContract` variable and calls contractService.ReadMethod once created. ReadMethod takes a callback method that will be triggered on successful read. We'll use ReadSuccess

```csharp
public void ReadContract()
{
    // Creates a ContractInfo object with the smart contract address, method name, network name, and default node URL
    var contractInfo = new ContractInfo(deployedContract, "[METHOD NAME]");

    // Calls the ReadMethod method to execute the smart contract method defined in the ABI with an empty input parameter
    contractService.ReadMethod(contractInfo, body, ReadSuccess, EmergenceLogger.LogError);
}
```

The `ReadSuccess` method is called when the `ReadMethod` method executes successfully. It logs the response to the console.

```csharp
private void ReadSuccess<T>(T response)
{
    Debug.Log($"{response}");
}
```

By following this example, you can read smart contracts in your Unity project using the EmergenceSDK. The process involves creating a `ContractInfo` object, and calling the `ReadMethod` to execute a smart contract method with the provided input data. This allows you to retrieve information from the smart contract without modifying its state, which is useful for displaying data in your application or making decisions based on the contract's current state.



Full code:

```csharp
using EmergenceSDK.Runtime.Internal.Utils;
using EmergenceSDK.Runtime.ScriptableObjects;
using EmergenceSDK.Runtime.Services;
using UnityEngine;

namespace EmergenceSDK.Samples.CoreSamples.Examples
{
    public class ReadingContracts : MonoBehaviour
    {
        [Header("Contract information")]
        // This must be set in the inspector
        public DeployedSmartContract deployedContract;
        // Public string array that is used as input data for the smart contract method
        public string[] body = new string[] { };

        private IContractService contractService;
        
        public void Awake()
        {
            contractService = EmergenceServiceProvider.GetService<IContractService>();
        }

        public void Start()
        {
            ReadContract();
        }

        private void ReadContract()
        {
            // Creates a ContractInfo object with the smart contract address, method name, network name, and default node URL
            var contractInfo = new ContractInfo(deployedContract, "[METHOD NAME]");

            // Calls the ReadMethod method to execute the smart contract method defined in the ABI with an empty input parameter
            contractService.ReadMethod(contractInfo, body, ReadSuccess, EmergenceLogger.LogError);
        }

        // This method is called when the ReadMethod method executes successfully
        private void ReadSuccess<T>(T response)
        {
            // Logs the response to the console
            EmergenceLogger.LogInfo($"{response}");
        }
    }
}

```
