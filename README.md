# Ubuntu22.04-DockerSetUp

## :warning: Clarification: Personal Local Setup Guide (Ubuntu 22.04 + Docker)
> Note: This guide is intended as a personal reference for setting up my local machine with Ubuntu 22.04 machine using Docker.

### :white_check_mark: **Enable Windows Subsystem for Linux**  

Open PowerShell as **Administrator** (Start menu > PowerShell > right-click > Run as **Administrator**) and enter this command:  

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart  
```  

### :information_source: Alternative way to Enable WSL
> Press **Window** button then search **Turn Windows feature On and Off**, **look for Windows Subsystem for Linux**  

