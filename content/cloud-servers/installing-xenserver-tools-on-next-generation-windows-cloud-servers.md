---
permalink: installing-xenserver-tools-on-next-generation-windows-cloud-servers/
node_id: 3232
title: Upgrade to XenServer Tools on Windows Cloud servers
type: article
created_date: '2012-12-07'
created_by: Jered Heeschen
last_modified_date: '2016-04-28'
last_modified_by: Hounsou Dansou
product: Cloud Servers
product_url: cloud-servers
---

### Supported Operating Systems

- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

An earlier version of the XenServer Tools software that is installed on First Generation Windows Servers has been found to cause server instability in rare cases.

To prevent any issues from occurring, follow the steps in this article to upgrade the XenServer Tools to the version 6.5 on First Generation servers that have been migrated to Next Generation.

We *strongly* recommend backing up any important data (and possibly taking a snapshot of your server) before attempting the installation, to be on the safe side.

### Upgrade, don't uninstall

If your cloud server is affected by this issue, *do not uninstall* the existing Citrix XenServer Tools package. Instead, upgrade the package in place.  Uninstalling the existing XenServer Tools software will render your server inaccessible.

### Affected instances

[nextcp]:https://mycloud.rackspace.com

This issue affects only First Generation servers that have been migrated to Next Generation.  First Generation Cloud Servers (which appear with asterisks next to their names in the [Cloud Control Panel][nextcp] are not affected.

To determine whether you need to upgrade to a newer version of XenServer Tools installed, check your current version in the Windows Control Panel, under **Programs and Features**.

If the listed version is earlier than 6.5 you should upgrade.

Note that the upgrade requires several reboots of your instance to complete the process.

### Upgrade to XenServer Tools 6.5

Before installation the Xenserver Tools 6.5, the Windows Agent must be upgraded first, which allows the Xentools tools to reset the network appropriately during the upgrade process.

The following command should be executed from the command prompt. Once executed, it will download the latest version of the Windows Agent and upgrade it if needed. It will also download the XenServer Tools 6.5 and place it under the folder `C:\rs-pkgs\xs-tools-6.5.0-20200-agent\` where you will execute the installer `install.bat`.

```
powershell.exe -NoProfile -NoLogo -InputFormat None -ExecutionPolicy Bypass -Command "iex(New-Object Net.WebClient).DownloadString('http://b2566e7bb4c60838ad8e-2feac036ecfab0eba46621f3ae4943bc.r28.cf1.rackcdn.com/latest/Update-Xentools.ps1')"
```

After executing the command above, it will generate an output similar to the one below.

```
[04/28/2016 21:18:15] Info  :: STEP 1 => Update the Nova Agent
[04/28/2016 21:18:16] Info  :: Starting the Agent Upgrade to version 1.3.1.1
[04/28/2016 21:18:16] Warn  :: RackspaceCloudServersAgent RackspaceCloudServersAgentUpdater is stopped
[04/28/2016 21:18:16] Info  :: Downloading the AgentService_1.3.1.1.zip
[04/28/2016 21:18:17] Info  :: Downloaded Successfully AgentService_1.3.1.1.zip in  C:\Windows\Temp
[04/28/2016 21:18:17] Info  :: Downloading the UpdateService_1.3.1.1.zip
[04/28/2016 21:18:18] Info  :: Downloaded Successfully UpdateService_1.3.1.1.zip in  C:\Windows\Temp
[04/28/2016 21:18:18] Info  :: Renaming Agent to 1.3.0.3
[04/28/2016 21:18:18] Info  :: Renaming AgentUpdater to 1.3.0.3
[04/28/2016 21:18:18] Info  :: Unzipping AgentService.zip to Agent)
[04/28/2016 21:18:18] Info  :: Creating the Directory C:\Program Files\Rackspace\Cloud Servers\Agent
[04/28/2016 21:18:18] Info  :: Unzipping UpdateService.zip to AgentUpdater
[04/28/2016 21:18:18] Info  :: Creating the Directory C:\Program Files\Rackspace\Cloud Servers\AgentUpdater
[04/28/2016 21:18:18] Info  :: Cloning the AgentLog from Agent1.3.0.3 to Agent
[04/28/2016 21:18:18] Info  :: Removing AgentService_1.3.1.1.zip and UpdateService_1.3.1.1.zip
[04/28/2016 21:18:18] Info  :: Restarting the Agent and AgentUpdater services
[04/28/2016 21:18:25] Info  :: STEP 1 => DONE!!!
                               *********************************************************************************
[04/28/2016 21:18:25] Info  :: STEP 2 => Download the latest XenServer Tools on the Server
[04/28/2016 21:18:31] Info  :: Downloaded Successfully xs-tools-6.5.0-20200-agent.zip in  C:\rs-pkgs
[04/28/2016 21:18:31] Info  :: Creating the Directory C:\rs-pkgs\xs-tools-6.5.0-20200-agent
[04/28/2016 21:18:32] Info  :: STEP 2 => DONE!!!
[04/28/2016 21:18:32] Info  :: *********************************************************************************
[04/28/2016 21:18:32] Info  :: STEP 3 => Before executing the installation of the Xenserver Tools,
                               YOU MUST CREATE A SNAPSHOT OF YOUR SERVER using the Control Panel
                               The Snapshot will allow you to recover your server if the installation fails.
                               Once you are done with This Step 3, Start the installation at STEP 4
                               *********************************************************************************
[04/28/2016 21:18:32] Warn  :: STEP 4 => Execute the Xenserver tools Installer.
                               Before you execute the installer, connect to the Console of the server
                               in the Control Panel, because the server will reboot few times on its own.
                               You will loose network access and Remote Desktop will fail
                               until the installation is completed.
                               *********************************************************************************
                               Execute:  C:\rs-pkgs\xs-tools-6.5.0-20200-agent\install.bat
                               *********************************************************************************
```



 After the instance has rebooted, confirm that the upgrade was successful by checking the version of XenServer Tools in Programs and Features, as described earlier. The version should now be 6.5.


