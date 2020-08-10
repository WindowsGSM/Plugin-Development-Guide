# Plugin-Development-Guide
🧩 WindowsGSM Plugin Development Guide - Support more game servers by creating and installing plugins!


#### Support server
https://discord.gg/bGc7t2R

#### Table of Contents:
1. [Introduction](#Introduction)
1. [Basic Knowledge](#Knowledge)
1. [Set up a plugin development environment](#Set-up-a-plugin-development-environment) 
1. [Creating Your First Plugin](#Creating-your-first-plugin) 
1. [Testing Your First Plugin](#Testing-your-first-plugin) 

<a name="Introduction"/>

## Introduction
[WindowsGSM](https://github.com/WindowsGSM/WindowsGSM) (**>= 1.21.0**) starts supporting plugins installation since users want to add their own game servers to WindowsGSM which WindowsGSM doesn't support those game servers yet. More importantly, users can wait for a plugin release on the community instead of WindowsGSM release. 

> (27/01/2020) **! AssaultLine** says... _We need to know if its possible to add a game now in a custom way._

> (14/04/2020) **Redyear20** says... _I want to know if this game panel is capable to add games not listed. For example I want to add The Isle_

> (20/07/2020) **Kratomasy 🌈 aka Alaric** says... _is there a way to add a custom steam game server that is not in the list of GSM?_

> (06/08/2020) **Tempus Thales** says... _If I wanted to add a server that is not listed in your tool, can I still add it with your tool?_

> (09/08/2020) WindowsGSM v1.21.0 released! 🥳

<a name="Knowledge"/>

## Basic Knowledge
✔ Before writing plugins, lets understand how it looks like and how it works. 

#### How plugins works?
WindowsGSM scan the plugins folder and loads **{PLUGIN_NAME}.cs**, **{PLUGIN_NAME}.png** and **author.png** files of each plugin.

##### The plugin file structure is basically like that: (Installed [WindowsGSM.ARMA3](https://github.com/BattlefieldDuck/WindowsGSM.ARMA3) and [WindowsGSM.PaperMC](https://github.com/BattlefieldDuck/WindowsGSM.PaperMC))

![Plugin File Structure](https://windowsgsm.com/assets/images/WindowsGSM-PluginsFileStructure-v1.21.0.png)

##### For **WindowsGSM.PaperMC** plugin, WindowsGSM reads folder **PaperMC.cs** and loads **PaperMC.cs**, **PaperMC.png** and **author.png**
![Plugin File Structure](https://windowsgsm.com/assets/images/plugin-demos/PaperMC-files-usage.png)

<a name="Set-up-a-plugin-development-environment"/>

## Set up a plugin development environment
Now let's set up a plugin development environment.

#### Prerequisites
1. [.NET Framework 4.7.2](https://dotnet.microsoft.com/download/dotnet-framework/net472)
1. [Visual Studio 2019](https://sr.gdprvalidate.de/redir/clickGate.php?u=8otB939m&m=12&p=3b121G4eNI&t=33&splash=0&s=&url=https%3A%2F%2Fvisualstudio.microsoft.com%2Fzh-hant%2Fdownloads%2F)

#### Preparations
Download or git pull the latest WindowsGSM #master (https://github.com/WindowsGSM/WindowsGSM)

#### Get Started
Open **WindowsGSM.sln** with Visual Studio 2019

##### You should see something like this
![](https://windowsgsm.com/assets/images/plugin-demos/vs-plugins.png)

The plugin development environment is set up! 🥳

<a name="Creating-your-first-plugin"/>

## Creating Your First Plugin
As you know, most game servers use steamcmd to install and update the server. WindowsGSM already created [SteamCMDAgent](https://github.com/WindowsGSM/WindowsGSM/blob/master/WindowsGSM/GameServer/Engine/SteamCMDAgent.cs) class for inheritance purpose, so adding a game server that uses steamcmd is much easier than adding a server that does not support steamcmd.

### 1. Create a new plugin script
Create a **MyFirstPlugin.cs** file inside **Plugins** folder on WindowsGSM-Plugin-Development project

### 2. Edit the plugin script
#### Add WindowsGSM references
```cs
using WindowsGSM.Functions;
using WindowsGSM.GameServer.Engine;
using WindowsGSM.GameServer.Query;
using Newtonsoft.Json.Linq;
```

#### Change the namespace to WindowsGSM.Plugins
```cs
namespace WindowsGSM.Plugins
```

#### Setting up plugin info
```cs
public Plugin Plugin = new Plugin
{
    name = "WindowsGSM.XXXXX",
    author = "Your name",
    description = "🧩 WindowsGSM plugin for supporting XXXXXX Server",
    version = "1.0",
    url = "https://github.com/XXXXXXXX/XXXXXXXX",
    color = "#ffffff"
};
```

#### Continue read ...

<details>
  <summary>Plugin Format that inherits SteamCMDAgent</summary>
  
  #### Set SteamCMDAgent as parent 
  ```cs
  public class MyFirstPlugin : SteamCMDAgent
  ```
  
  #### Add constructor and properties
  ```cs
  public MyFirstPlugin(ServerConfig serverData) : base(serverData) => base.serverData = _serverData = serverData;
  private readonly ServerConfig _serverData;
  ```
  
  #### Add properties for SteamCMD installer
  ```cs
  public override bool loginAnonymous => false; // true if allows login anonymous on steamcmd, else false
  public override string AppId => ""; // Value of app_update <AppId> 
  ```
  
  #### Add standard variables
  ```cs
  public override string StartPath => ""; // Game server start path
  public string FullName = ""; // Game server FullName
  public bool AllowsEmbedConsole = false;  // Does this server support output redirect?
  public int PortIncrements = 1; // This tells WindowsGSM how many ports should skip after installation
  public object QueryMethod = null; // Query method. Accepted value: null or new A2S() or new FIVEM() or new UT3()

  public string Port = ""; // Default port
  public string QueryPort = ""; // Default query port
  public string Defaultmap = ""; // Default map name
  public string Maxplayers = ""; // Default maxplayers
  public string Additional = ""; // Additional server start parameter
  ```
  
  #### Add standard functions
  ```cs
  public async void CreateServerCFG() { } // Creates a default cfg for the game server after installation

  public async Task<Process> Start() { return null; } // Start server function, return its Process
  public async Task Stop(Process p) { } // Stop server function
  ```
  
  Done! All necessary variables and functions were all created. you can now start edit your script and create your first plugin!
  
  #### Example plugin with plugin format that inherits SteamCMDAgent: [WindowsGSM.ARMA3](https://github.com/BattlefieldDuck/WindowsGSM.ARMA3)
  
</details>

<details>
  <summary>Classic Plugin Format</summary>

  #### Add constructor and properties
  ```cs
  public MyFirstPlugin(ServerConfig serverData) => _serverData = serverData;
  private readonly ServerConfig _serverData;
  public string Error, Notice;
  ```

  #### Add standard variables
  ```cs
  public string StartPath = ""; // Game server start path
  public string FullName = ""; // Game server FullName
  public bool AllowsEmbedConsole = false;  // Does this server support output redirect?
  public int PortIncrements = 1; // This tells WindowsGSM how many ports should skip after installation
  public object QueryMethod = null; // Query method. Accepted value: null or new A2S() or new FIVEM() or new UT3()

  public string Port = ""; // Default port
  public string QueryPort = ""; // Default query port
  public string Defaultmap = ""; // Default map name
  public string Maxplayers = ""; // Default maxplayers
  public string Additional = ""; // Additional server start parameter
  ```

  #### Add standard functions
  ```cs
  public async void CreateServerCFG() { } // Creates a default cfg for the game server after installation

  public async Task<Process> Start() { return null; } // Start server function, return its Process
  public async Task Stop(Process p) { } // Stop server function
  public async Task<Process> Install() { return null; } // Install server function
  public async Task<Process> Update() { return null; } // Update server function

  public bool IsInstallValid() { return false; } // Check if the installation is successful
  public bool IsImportValid(string path) { return false; } // Check is the directory valid for import

  public string GetLocalBuild() { return ""; } // Return local server version
  public async Task<string> GetRemoteBuild() { return ""; } // Return latest server version
  ```
  
  Done! All necessary variables and functions were all created. you can now start edit your script and create your first plugin! 
  
  #### Example plugin with classic plugin format: [WindowsGSM.PaperMC](https://github.com/BattlefieldDuck/WindowsGSM.PaperMC)
  
</details>

<a name="Testing-your-first-plugin"/>

## Testing Your First Plugin

![Install Plugin](https://windowsgsm.com/assets/images/plugin-demos/install-plugins.png)

1. Set **Startup Project** to **WindowsGSM-Plugin-Development** and click **Start** to start installing your plugins.
1. Set **Startup Project** to **WindowsGSM** and click **Start** to start WindowsGSM and start debug!
