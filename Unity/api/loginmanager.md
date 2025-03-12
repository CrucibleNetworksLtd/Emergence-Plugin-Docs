---
title: LoginManager
description: This Class manages Wallet connection with Emergence Services
parent: APIs
grand_parent: Unity Plugin
---

# LoginManager

#### Properties

**`bool cancelLoginsUponDisabling`**

Indicates whether login attempts should automatically be canceled when the `MonoBehaviour` is disabled.

**`bool IsBusy`**

Indicates whether the `LoginManager` is currently handling a login session.

**`EmergenceQrCode CurrentQrCode`**

Gets the currently active instance of `EmergenceQrCode` for the login session.

#### Events

**`LoginStartedEvent loginStartedEvent`**

Called after `StartLogin` is initiated, if `IsBusy` is false.

**`LoginCancelledEvent loginCancelledEvent`**

Called after `CancelLogin` is invoked, if `IsBusy` is true.

**`LoginFailedEvent loginFailedEvent`**

Called when an error occurs during login.

**`LoginSuccessfulEvent loginSuccessfulEvent`**

Called after a successful login. This event is intended for UI purposes; business logic should be handled in `ISessionService.OnSessionConnected`.

**`LoginStepUpdatedEvent loginStepUpdatedEvent`**

Called at each login step, useful for updating the UI. It is triggered both when a step begins and after it succeeds.

**`LoginEndedEvent loginEndedEvent`**

Called when the login process ends, regardless of the outcome.

**`QrCodeTickEvent qrCodeTickEvent`**

Ticks every second after the QR code is retrieved. This continues until right before `loginEndedEvent` is invoked.

#### Public Methods

**`void SetFirstLoginFlag()`**

Sets the first-login flag to true.

**`void ResetFirstLoginFlag()`**

Sets the first-login flag to false.

**`bool GetFirstLoginFlag()`**

Checks whether the first-login flag is present and set to a non-zero value.

**`UniTask StartLogin(LoginSettings loginSettings)`**

Starts a login attempt with the specified settings. Will not start if another attempt is ongoing.

**`void CancelLogin()`**

Cancels the current login attempt and triggers the appropriate events. This only works if there is an ongoing login attempt.

**`UniTask Disconnect()`**

Handles the disconnection process by invoking the appropriate disconnection events. This method will wait until the login process is complete before proceeding.

**`UniTask WaitUntilAvailable(CancellationToken ct = default)`**

Waits until the `IsBusy` property is false, indicating that no login attempts are in progress. A cancellation token can be provided to customize the wait time.

**`void RemoveAllListeners()`**

Clears all event listeners associated with the `LoginManager`.
