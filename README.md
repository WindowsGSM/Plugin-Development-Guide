# Plugin-Development-Guide
🧩 WindowsGSM Plugin Development Guide - Support more game servers by creating and installing plugins!

#### Table of Contents:
1. [Introduction](#Introduction)  
1. [Basic Knowledge](#Knowledge)  

<a name="Introduction"/>

## Introduction
[WindowsGSM](https://github.com/WindowsGSM/WindowsGSM) (**>= 1.21.0**) starts supporting plugins installation since users want to add their own game servers to WindowsGSM which WindowsGSM doesn't support those game servers yet. More importantly, users can wait for a plugin release on the community instead of WindowsGSM release. 

> (27/01/2020) **! AssaultLine** says... _We need to know if its possible to add a game now in a custom way._

> (14/04/2020) **Redyear20** says... _I want to know if this game panel is capable to add games not listed. For example I want to add The Isle_

> (20/07/2020) **Kratomasy 🌈 aka Alaric** says... _is there a way to add a custom steam game server that is not in the list of GSM?_

> (06/08/2020) **Tempus Thales** says... _If I wanted to add a server that is not listed in your tool, can I still add it with your tool?_

> (09/08/2020) WindowsGSM v1.21.0 released!

<a name="Knowledge"/>

## Basic Knowledge
WindowsGSM scan the plugins folder and loads **{PLUGIN_NAME}.cs**, **{PLUGIN_NAME}.png** and **author.png** files of each plugin.

##### The plugin file structure is basically like that: (Installed [WindowsGSM.ARMA3](https://github.com/BattlefieldDuck/WindowsGSM.ARMA3) and [WindowsGSM.PaperMC](https://github.com/BattlefieldDuck/WindowsGSM.PaperMC))

![Plugin File Structure](https://windowsgsm.com/assets/images/WindowsGSM-PluginsFileStructure-v1.21.0.png)

##### For **WindowsGSM.PaperMC** plugin, WindowsGSM reads folder **PaperMC.cs** and loads **PaperMC.cs**, **PaperMC.png** and **author.png**
![Plugin File Structure](https://windowsgsm.com/assets/images/plugin-demos/PaperMC-files-usage.png)
