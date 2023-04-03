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

- git clone https://github.com/mabubakarriaz/blogi-backend.git

- docker pull mcr.microsoft.com/dotnet/aspnet:7.0
- docker pull mcr.microsoft.com/dotnet/sdk:7.0
- docker build -t abubakarriaz/blogi-backend:latest .
- docker run -d -p 8100:80 --name blogi-backend-server-01 abubakarriaz/blogi-backend:latest
