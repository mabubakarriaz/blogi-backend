# Instrctions

- git clone https://github.com/mabubakarriaz/blogi-backend.git

- docker pull mcr.microsoft.com/dotnet/aspnet:7.0
- docker pull mcr.microsoft.com/dotnet/sdk:7.0
- docker build -t abubakarriaz/blogi-backend:latest .
- docker run -d -p 8100:80 --name blogi-backend-server-01 abubakarriaz/blogi-backend:latest
