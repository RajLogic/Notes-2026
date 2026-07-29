---
layout: "default"
title: "COSC2759 Week 2 - Lab"
---
 #devops
## Goals
* Have a basic understanding of DevOps
* Install the required software for the course

## Introduction (~5 mins) 

* Tutors introduce themselves as well as the course and how things will generally run this semester

## Discussion (~30 mins) 
 
* What is DevOps? 
* Why do you want to learn about DevOps? 
* What are some of the tools that you would use in DevOps? 
* How do we benefit from it? 
* Why do Agile and DevOps work so well together? 
* How has the cloud helped popularise DevOps? 
* What are some examples where the principle "Everything as code" doesn't apply? 
* What are some of the things you would measure in DevOps? 

## Configuring Tools (remainder)

By the end of the lab you should be able to run the following in your development environment: 

```bash
echo "Validating that we have the tools we need for SDO..."
git --version
python --version
curl --version
jq --version
terraform --version
aws --version
ansible --version
node --version
npm --version
docker --version
echo "OK"
```

### Installing Visual Studio Code

Install the appropriate version of [Visual Studio Code](https://code.visualstudio.com/Download) for your machine. 

Any text editor will work for this course, but VS Code will make your life easier as it has some quite nifty features and extensions. 

Feel free to use any editor, however any instructions / screenshots / demos will likely be using VS Code.


### Installing Tools

Depending on your operating system you will need to pick a "path" to follow. 

If you use macOS then just continue on with the lab sheet and stop once you reach the "Windows Path" section.

If you use Windows then scroll down to the "Windows Path" section and finish the lab sheet from there.

If you use Linux / UNIX then you should not need any help getting these tools installed! If in any trouble just follow the Windows instructions as we install the tooling inside a Linux VM.

### Mac Path

#### Git

First we need to install and setup Git. Download the git binary using homebrew:

```bash
brew install git
```

We now need to configure secure GitHub access from our machine. [What is GitHub?](https://docs.github.com/en/get-started/start-your-journey/about-github-and-git)

For this we are going to use SSH Keys. Essentially we will upload our public key to GitHub, when we push code we authenticate with GitHub using the private key stored only on our machine, which GitHub then verifies us, using the 
public key and approves our commits. 

Start by creating an SSH Key on your machine (ensure to use your student email):

```bash
ssh-keygen -t ed25519 -C "s123456789@student.rmit.edu.au" -f ~/.ssh/github_ssh_key
```

> The '~' is a shortcut that represents the Home directory of the currently logged in user, e.g. /Users/john.
>
> So the full file path of ~/.ssh/github_ssh_key would actually be /Users/john/.ssh/github_ssh_key (assuming john was logged in)

Accept all the default prompts after this to create it without a passphrase.

Once created we then need to create an SSH config file to instruct our machine to use our private key when authenticating with GitHub.

Create a file at `~/.ssh/config` with the following contents:

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github_ssh_key
  PreferredAuthentications publickey
```

Add the **public** SSH key to your GitHub account using your web browser. [GitHub Instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account)

The link above should provide the most up-to-date methods but the steps below should work too:
1. Click your profile > Settings
2. In "Access" click "SSH and GPG keys"
3. Click "New SSH Key"
4. In title enter something descriptive (e.g. "Mac Laptop")
5. Leave key type
6. In the key field paste the contents of your public key (`~/.ssh/github_ssh_key.pub`)
7. Click "Add SSH Key"

Test the connection by running `ssh -T git@github.com`. The first time this is run you will need to accept a host authenticity warning (type 'yes') and then you should see the following message:
```bash
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

#### Python

Install Python using brew:

```bash
brew install python
```

#### jq

Install jq using brew:

```bash
brew install jq
```

#### Terraform

Install terraform using brew:

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

#### Ansible

Install Ansible using brew:

```bash
brew install ansible
```

#### AWS Cli

Install AWS CLI using brew:

```bash
brew install awscli
```

#### Node

Install Node using brew, any version will be fine so if already installed there is no need to upgrade:

```bash
brew install node
```

> If you want to have multiple versions of Node installed then look into installing and using the Node Version Manager (NVM) 

#### Docker

Install from the following location: https://docs.docker.com/desktop/setup/install/mac-install/

### Windows Path

For those students on a Windows machine we are going to use the Windows Subsystem for Linux (WSL) to store and run all our work for this course. WSL gives us a Linux VM though which we can use Linux programs and commands, though a terminal, right here on Windows! VS Code also gives us nice features such as being able to open folders in our Linux environment using the WSL extension. 

To get started we first need to install WSL and then *inside* WSL setup all the tools we need for the semester. 

To install WSL open a PowerShell Window as an Admin and then run the following:

```powershell
wsl --install -d Ubuntu-26.04
```

> In this command we are installing the latest LTS (Long Term Support) version of Ubuntu but any recent version will do, if you already have a version installed don't worry about installing another one.

Once the program finishes installing WSL and the Ubuntu distribution it will open a console window and it will ask you to enter a unix username and password. The recommendation is to use your Windows username and password so you don't forget them. 

Once done you can reopen WSL anytime by searching for the "Ubuntu" program in the Start menu.

From now on all of the below instructions **should be run in WSL**.

#### Git

First we need to install and setup Git. Download the git binary using apt:

```bash
sudo apt update
sudo apt install git -y
```

We now need to configure secure GitHub access from our machine. [What is GitHub?](https://docs.github.com/en/get-started/start-your-journey/about-github-and-git)

For this we are going to use SSH Keys. Essentially we will upload our public key to GitHub, when we push code we authenticate with GitHub using the private key stored only on our machine, which GitHub then verifies using the 
public key and approves our commits. 

Start by creating an SSH Key on your machine (ensure to use your student email):

```bash
ssh-keygen -t ed25519 -C "s123456789@student.rmit.edu.au" -f ~/.ssh/github_ssh_key
```

> The '~' is a shortcut that represents the Home directory of the currently logged in user, e.g. /home/john.
>
> So the full file path of ~/.ssh/github_ssh_key would actually be /home/john/.ssh/github_ssh_key (assuming john was logged in)

Accept all the default prompts after this to create it without a passphrase.

Once created we then need to create an SSH config file to instruct our machine to use our private key when authenticating with GitHub.

Create a file at `~/.ssh/config` with the following contents:

> As we are in a terminal environment we can use Nano as a console based text editor. 
>
> Run `nano ~/.ssh/config` to create the config file and open it with Nano. Use the keyboard or paste the contents in and then following the instructions to save and close Nano (Ctrl + O, Ctrl + X).

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github_ssh_key
  PreferredAuthentications publickey
```

Update the file permissions of the config file: 

```bash
chmod 600 ~/.ssh/config
```

Add the **public** SSH key to your GitHub account using your web browser. [GitHub Instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account)

The link above should provide the most up-to-date methods but the steps below should work too:
1. Click your profile > Settings
2. In "Access" click "SSH and GPG keys"
3. Click "New SSH Key"
4. In title enter something descriptive (e.g. "Mac Laptop")
5. Leave key type
6. In the key field paste the contents of your public key (`~/.ssh/github_ssh_key.pub`). To view the content we can use the cat command (`cat ~/.ssh/github_ssh_key.pub`)
7. Click "Add SSH Key"

Test the connection by running `ssh -T git@github.com`. The first time this is run you will need to accept a host authenticity warning (type 'yes') and then you should see the following message:
```bash
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

#### Python

Python should be installed by default, verify using:

```bash
python3 --version
```

If not present lets install it: 

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv -y
```

#### jq

Install jq using apt:

```bash
sudo apt install jq -y
```

#### Terraform

Install terraform using apt with the instructions from Hasicorp: https://developer.hashicorp.com/terraform/install#linux

#### Ansible

Install Ansible using apt with the instructions from RedHat: https://docs.ansible.com/projects/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu

#### AWS Cli

Install AWS CLI using the following commands:

```bash
cd ~
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install zip unzip -y
unzip awscliv2.zip
sudo ./aws/install
```

#### Node

Install Node using the Node Version manager

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.5/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 24
```

> If you get a error saying that the NVM command can't be found simply close your Ubuntu terminal and re-open it.

#### Docker

Install the docker engine using the following commands:

```bash
cd ~
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
```