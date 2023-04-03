# Objective

Please perform the following assignment project on Azure by using ACloud Guru Sandbox, and record screen videos after completion of every activity.

- Pick any open source .net project or.net core from the internet
- Front End sample on angular
- Choose a sample db SQL based
- Create a docker file for these
- Setup Azure DevOps CI/CD pipelines
- Create an Azure Architecture diagram, and choose wisely it is totally up to you how you want to deploy and host 
- DB should be in a private subnet and cant be accessible over the internet
- Configure SSL on the domain, you can use a custom subdomain from tkxel-team.com
- Setup DNS on CloudFlare
- You can choose any web server

## Instructions

## Service Connections

- Project Settings > Service Connections > Create Service Connection
- Connections Required
  - Github
    - mabubakarriaz
  - Docker Hub
    - docker-registry
  - SSH a VM
    - ssh-vm

## Web VM Setup

- Create linux vm
- Select web subnet
- Install docker by following below ```Docker Setup```.
- Install sql client by following below ```SQL CMD setup```.

## Database

- create sql server instance
- create sql database
- Create vnet service end point with microsoft.sql
- create private end point for sql
- create private DNS entry

## Build Agent Setup

- Create Personal Access Token (PAT) from Azure DevOps
  - User Settings > Personal Access Tokens > New Token > Scope > 'full access'
- Create a VM build agent
  - Project Settings > Agent Pools > Default > New Agent > Linux
  
- Download agent
  
  ```sh
  wget https://vstsagentpackage.azureedge.net/agent/3.218.0/vsts-agent-linux-x64-3.218.0.tar.gz
  ```

- Create the agent ( the file name may be updated see online instructions)
  
  ```sh
  mkdir myagent && cd myagent
  tar zxvf ~/vsts-agent-linux-x64-3.218.0.tar.gz
  ```

- Configue agent

  ```sh
  ./config.sh
  ```

- Run the agent interactively (TODO: write steps to run agent non-interactively)

  ```sh
  ./run.sh
  ```

- Install docker by following below ```Docker Setup```.
- To speed up pull these images

  ```sh
  docker pull mcr.microsoft.com/dotnet/aspnet:7.0
  docker pull mcr.microsoft.com/dotnet/sdk:7.0
  ```

- run the interactive agent runner ```./run.sh```



### Docker Setup

Script to setup docker on linux vm by using https://docs.docker.com/engine/install/ubuntu/

- ssh into vm
  
  ```sh
  ssh -i vm-key.pem azureuser@123.123.123.123
  ```

- Uninstall old versions
  
  ```sh
  sudo apt-get remove docker docker-engine docker.io containerd runc
  ```

- Update the apt package index and install packages to allow apt to use a repository over HTTPS:

  ```sh
  sudo apt-get update
  sudo apt-get install \
      ca-certificates \
      curl \
      gnupg
  ```

- Add Docker’s official GPG key:

  ```sh
  sudo mkdir -m 0755 -p /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  ```

- Use the following command to set up the repository:

  ```sh
  echo \
    "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```

- Grant access to gpg

  ```sh
  sudo chmod a+r /etc/apt/keyrings/docker.gpg
  sudo apt-get update
  ```

- Install Docker Engine, containerd, and Docker Compose.

  ```sh
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

- Grant running use access

  ```sh
  sudo usermod -aG docker $(whoami)
  sudo service docker restart
  ```

- verify by runing container

  ```sh
  sudo docker run hello-world
  ```

### SQL CMD setup

Script to setup sql cmd utilities on vm using link https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?tabs=ubuntu-install%2Credhat-offline&view=sql-server-ver16#ubuntu

- ssh into vm
  
  ```sh
  ssh -i vm-key.pem azureuser@123.123.123.123
  ```

- Import the public repository GPG keys.
  
  ```sh
  curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
  ```

- Register the Microsoft Ubuntu repository.
  
  ```sh
  curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
  ```

- Update the sources list and run the installation command with the unixODBC developer package.

  ```sh
  sudo apt-get update
  sudo apt-get install mssql-tools unixodbc-dev
  ```

- To make sqlcmd/bcp accessible from the bash shell for login sessions

  ```sh
  echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
  ```

- To make sqlcmd/bcp accessible from the bash shell for interactive/non-login sessions,

  ```sh
  echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
  source ~/.bashrc
  ```

- connection string from vm
  
  ```sh
  sqlcmd -S tcp:blogisqlserver003223.database.windows.net,1433 -d AdventureWorksLT -U azureuser -P myPassword
  ```

### Important commands

- docker build -t abubakarriaz/blogi-backend:latest .
- docker run -d -p 8100:80 --name blogi-backend-server-01 abubakarriaz/blogi-backend:latest
- git clone https://github.com/mabubakarriaz/blogi-backend.git
- ssh -i vm-key.pem azureuser@123.123.123.123
- sqlcmd -S myservername,1433 -d mydbname -U azureuser -P myPassword