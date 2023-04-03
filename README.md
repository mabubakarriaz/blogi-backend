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

# Instructions

## Service Connections

- Github
  - mabubakarriaz
- Docker Hub
  - docker-registry
- SSH a VM
  - ssh-vm

## Build Agent Setup

- Create a VM build agent
- Create Personal Access Token (PAT) from Azure DevOps
- Go to download instructions on Create new default agent for linux
- Install docker as instructions from https://docs.docker.com/engine/install/ubuntu/
- Give rights sudo usermod -aG docker $(whoami)
- sudo service docker restart
- run the interactive agent runner ./run.sh

## Web VM Setup

- Install docker as instructions from https://docs.docker.com/engine/install/ubuntu/
- Install docker as instructions from https://docs.docker.com/engine/install/ubuntu/
- Give rights sudo usermod -aG docker $(whoami)
- sudo service docker restart
- To speed up pull these images
  - docker pull mcr.microsoft.com/dotnet/aspnet:7.0
  - docker pull mcr.microsoft.com/dotnet/sdk:7.0
- Setup sql connectivity  go to: https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?tabs=ubuntu-install%2Credhat-offline&view=sql-server-ver16#ubuntu
- connection string from vm: sqlcmd -S tcp:blogisqlserver003223.database.windows.net,1433 -d AdventureWorksLT -U azureuser -P Mobilink@@123456

## Database

- create sql server instance
- create sql database
- Create vnet service end point with microsoft.sql
- create private end point for sql
- create private DNS entry

### important commands

- docker build -t abubakarriaz/blogi-backend:latest .
- docker run -d -p 8100:80 --name blogi-backend-server-01 abubakarriaz/blogi-backend:latest
- git clone https://github.com/mabubakarriaz/blogi-backend.git
