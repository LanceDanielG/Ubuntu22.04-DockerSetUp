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

### :information_source: Alternative way to Install (Command Line)
> If you prefer the terminal or don't have access to the Store app:

```bash
wsl --list --online
wsl --install -d Ubuntu-22.04
```

### :white_check_mark: Set Up Ubuntu (First Run)

You'll be promted to:  
*  Enter a new UNIX username
*  Enter and confirm a new password  

## :information_source: Run this to Ubuntu 22.04 Terminal

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

## :white_check_mark: Run Docker Without `sudo`
> :information_source: This allows you to run Docker commands without needing to prepend `sudo` every time.
```bash
sudo usermod -aG docker $USER
newgrp docker
```

## :white_check_mark: Check if Docker is running
> Run the `hello-world` image to verify that Docker is correctly installed and configured.
```bash
docker run hello-world
```

## :information_source: Optional Tools to the Set Up
`Install Git`
```bash
sudo apt install git
```

`Configure Git`
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

`Generate SSH Key`
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
cat ~/.ssh/id_ed25519.pub
```

`Install NVM and Node`
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm alias default node
```

### :rocket: Tip: Auto-switch Node Version
> Add this to your shell configuration (`~/.bashrc` or `~/.zshrc`) to automatically switch Node versions when you `cd` into a directory with an `.nvmrc` file.

**Bash (Default for Ubuntu)**
Run this command to append the configuration to your `~/.bashrc` and reload it:
```bash
cat << 'EOF' >> ~/.bashrc

# Auto-switch Node Version
cdnvm() {
    cd "$@";
    nvm_path=$(nvm_find_nvmrc);
    if [ -n "$nvm_path" ]; then
        nvm use || nvm install;
    fi
}
alias cd='cdnvm'
EOF
source ~/.bashrc
```

**Zsh (Alternative Shell)**
Run this command to append the configuration to your `~/.zshrc` and reload it:
```bash
cat << 'EOF' >> ~/.zshrc

# Auto-switch Node Version
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -f "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "$nvmrc_path")")
    if [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use || nvm install
    fi
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
EOF
source ~/.zshrc
```

### :memo: How to create an `.nvmrc` file
Run this command in your project root to pin the current Node version:
```bash
node -v > .nvmrc
```
*Now, whenever you or anyone else `cd`s into this directory, the auto-switch script will ensure the correct Node version is used.*

## 📌 Tip: Launch Ubuntu & VS Code Easily
> You can install WSL extension in VS Code and work in your WSL Ubuntu environment seamlessly.