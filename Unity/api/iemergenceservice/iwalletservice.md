---
title: IWalletService
description: Service for interacting with the wallet API.
parent: IEmergenceService
---

# IWalletService

#### Properties

**`string WalletAddress`**

Gets the address of the wallet that is currently logged in.

**`string ChecksummedWalletAddress`**

Gets the checksummed address of the wallet that is currently logged in.

**`bool IsValidWallet`**

Indicates whether an address is currently logged in. Checks that `WalletAddress` and `ChecksummedWalletAddress` are not empty.

#### Methods

**`UniTask RequestToSign(string messageToSign, RequestToSignSuccess success, ErrorCallback errorCallback)`**

Attempts to sign a message using the WalletConnect protocol. The `RequestToSignSuccess` callback will return the signed message if successful.

**`UniTask GetBalance(BalanceSuccess success, ErrorCallback errorCallback)`**

Attempts to get the balance of the wallet. The `BalanceSuccess` callback will fire with the balance if successful.

**`UniTask ValidateSignedMessage(string message, string signedMessage, string address, ValidateSignedMessageSuccess success, ErrorCallback errorCallback)`**

Attempts to validate a signed message. The `ValidateSignedMessageSuccess` callback will fire with the validation result if the call is successful.
