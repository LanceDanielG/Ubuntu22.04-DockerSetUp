# Ubuntu22.04-DockerSetUp

## :warning: Clarification: Personal Local Setup Guide (Ubuntu 22.04 + Docker)
> Note: This guide is intended as a personal reference for setting up my local machine with Ubuntu 22.04 machine using Docker.

### :white_check_mark: Install WSL 

```bash
wsl --install
```

> If needed: 
### :white_check_mark: Enable Windows Subsystem for Linux and Virtual Machine Feature

Open PowerShell as **Administrator** (Start menu > PowerShell > right-click > Run as **Administrator**) and enter this command:  

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart  
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```  

### :information_source: Alternative way to Enable WSL and Virtual Machine
> Press **Window** button then search **Turn Windows feature On and Off**, **look for Windows Subsystem for Linux** and **Virtual Machine Platform**, then check and press OK. restart later.  

### :white_check_mark: Set WSL Version to 2  

```bash
wsl --set-default-version 2
```

### :information_source:  To check if WSL is set to version 2
Run this command:  

```bash
wsl -l -v
```

### :white_check_mark: Install Ubuntu 22.04 from Microsoft Store  

Open **Microsoft Store**, Search for: **Ubuntu 22.04** Click Install then Open to launch it.

### :white_check_mark: Set Up Ubuntu (First Run)

You'll be promted to:  
*Enter a new UNIX username
*Enter and confirm a new password


