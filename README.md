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
*  Enter a new UNIX username
*  Enter and confirm a new password  

## > :information_source: Run this to Ubuntu 22.04 Terminal

### :white_check_mark: Uninstall old versions
> Before you can install Docker Engine, you need to uninstall any conflicting packages.

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

### :white_check_mark: Install Docker in Ubuntu

`Update package info`
```bash
sudo apt update
```

`Install dependencies`
```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

`Add Docker’s official GPG key`
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

`Set up the repository`
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

`Update and install Docker`
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```



