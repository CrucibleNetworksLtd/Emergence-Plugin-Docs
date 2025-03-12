---
title: How to open and close the overlay
parent: Sample Code
---

# How to open / close the overlay

While the EmergenceSDK automatically handles opening and closing the overlay when using the provided prefab, there might be situations where you want more control over these actions in your application. This documentation page is designed to help you understand how to manually open and close the overlay.

### Opening the overlay screen

Instead of using the keyboard shortcut, the overlay can be opened by calling the following method from anywhere in your code.

```csharp
EmergenceSingleton.Instance.OpenEmergenceUI();
```

### Closing the overlay screen

Similarly, if for some reason your app needs to force the overlay closed the code to do it is the following:

```csharp
EmergenceSingleton.Instance.CloseEmergenceUI();
```
