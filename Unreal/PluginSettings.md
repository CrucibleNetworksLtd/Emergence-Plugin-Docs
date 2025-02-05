---
title: Plugin Settings
description: Settings for the Unreal SDK.
parent: Unreal Plugin
layout: default
---

# Plugin Settings

The plugin settings can be found in the project setting when the plugin is enabled. You don't need to set anything up to get started, this is just a reference for what each of them does (you can also see by hovering over each one in engine).

![](PluginSettings.png)

## General

### Debug/Development/Test build cloud environment

Which cloud environment should be communicated with when the game is built as "Debug", "Development" or "Test". Default is "Staging".

### Shipping build cloud environment

Which cloud environment should be communicated with when the game is built as "Shipping". Default is "Production".

## Futureverse

### Debug/Development/Test build Futureverse Cloud Environment

Which Futureverse cloud environment should be communicated with when the game is built as "Debug", "Development" or "Test". Default is "Production".

### Shipping build Futureverse cloud environment

Which Futureverse cloud environment should be communicated with when the game is built as "Shipping". Default is "Production".

### Futureverse Web Login Production Env Client ID

A custom client ID to use with the Futureverse web login flow on the Futureverse Production Environment. One of these can be created at https://login.futureverse.app/manageclients . Default is an empty string, which means you use Crucible's API key.

### Futureverse Web Login Staging Env Client ID

A custom client ID to use with the Futureverse web login flow on the Futureverse Development / Staging Environments. One of these can be created at https://login.futureverse.cloud/manageclients . Default is an empty string, which means you use Crucible's API key.

## IPFS

### Custom IPFS Node

The IPFS node to use when getting IPFS data via HTTP. Leaving it blank will use the default "http://ipfs.openmeta.xyz/ipfs/". The IPFS hash will be added to the end (for example, using the default: "http://ipfs.openmeta.xyz/ipfs/Qme7ss3ARVgxv6rXqVPiikMJ8u2NLgmgszg13pYrDKEoiu").

## LibCurl

### Allow LibCurl Connection Reuse

If true, libcurl will be allowed to "reuse connections". You probably want to leave this off unless it causes issues for your specific hardware, but it can speed up requests on some systems. If you toggle this, you may have to restart the editor for it to fully have an effect.
