---
title: Unreal Plugin
description: Requirements and installing the plugin.
nav_order: 1
---

# Getting Started

## Pre-Requisites

To use the Emergence Unreal Engine plugin, you will need the following:

* Windows or MacOS (Emergence only supports development and games on these platforms currently)
* Unreal Engine 5.4 or 5.5
* For Windows, the appropriate version of Visual Studio for the version of Unreal you wish to use (see [here for the versions for 5.1+](https://docs.unrealengine.com/5.3/en-US/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine/) and [here for 4.27-5.0](https://docs.unrealengine.com/5.1/en-US/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine/)).
* For MacOS, the [appropriate version of XCode](https://docs.unrealengine.com/5.2/en-US/macos-development-requirements-for-unreal-engine/) for the version of Unreal you wish to use with the [license accepted](https://apple.stackexchange.com/a/213151).

## Installation

*We have a sample project if you just want to skip to seeing everything working, check it out [here](../sample-project.md)!*

Extract the [Emergence plugin zip file](https://github.com/CrucibleNetworksLtd/emergence-plugin-unreal/releases) to your game’s plugin folder (if you don’t have a plugins folder, just create one called “Plugins” at the root folder of your game e.g. one one with Source, Saved, Content, etc). Extract the zip to this folder. It should look something like `[Your Game]/Plugins/Emergence/Emergence.uplugin`, for example.

Open your project. You may receive a window that looks like this:

![](<../../../.gitbook/assets/image (5) (3) (1).png>)

Press yes and wait for it to compile the modules. Your project should open (if it doesn’t, please send us the build log from `[Your Game]\Saved\Logs`).

When your game project opens, the plugin should be automatically enabled.

If you wish to use Emergence's C++ API from you're game's code, you'll need to:

* Add the Emergence modules you want to reference to your game's build.cs file 
* Set the C++ standard to 17 or higher

