# Ingesting data

- Download the dataset from "data\source\data.txt"
- Create a EC2 Instance with Ubuntu OS and Amazon Linux 2. 
- Configure the instance security group and assign a Elastic IP.
- Install Docker on the EC2 instance. 
- Docker Container > mcr.microsoft.com/mssql/server:2022-latest

```bash
# windows
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=FdeDeveloper12345678!' -p 1433:1433 --name legacy-mssql -d mcr.microsoft.com/mssql/server:2022-latest

# or multi-line in windows 
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=FdeDeveloper12345678!' ^
   -p 1433:1433 --name legacy-mssql ^
   -d mcr.microsoft.com/mssql/server:2022-latest

# linux / Mac
# Single
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=FdeDeveloper12345678!' -p 1433:1433 --name legacy-mssql -d mcr.microsoft.com/mssql/server:2022-latest

# or multi-line unix
docker run \
  -e 'ACCEPT_EULA=Y' \
  -e 'MSSQL_SA_PASSWORD=FdeDeveloper12345678!' \
  -p 1433:1433 \
  --name legacy-mssql \
  -d \
  mcr.microsoft.com/mssql/server:2022-latest
```

```bash
# Multi-line with volume inside AWS EC2
docker run \
  -v mssql_data:/var/opt/mssql \
  -e 'ACCEPT_EULA=Y' \
  -e 'MSSQL_SA_PASSWORD=FdeDeveloper12345678!' \
  -p 1433:1433 \
  --name legacy-mssql \
  -d \
  mcr.microsoft.com/mssql/server:2022-latest

```


- install the req > uv pip install -r requirements.txt

- python scripts\ingest_legacy_data.py

**Docker Commands**

```bash
docker ps
docker ps -a
docker stop [container_name or container_id]
docker rm [container_name or container_id] # Container
docker rmi [image_name] # Image
docker volume ls # Volume
docker volume rm [volume_name] # Volume
```

```bash
brew update
brew upgrade
brew install unixodbc
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew trust --formula microsoft/mssql-release/msodbcsql18
brew install msodbcsql18
brew install openssl@3

```


```bash
# Python commands
python3 -m venv .venv
source .venv/bin/activate

# uv commands
uv add pandas pyodbc
uv add -r requirements.txt

# Install requirements
uv pip install -r requirements.txt

# Deactivate
deactivate
```

## Install SQL Server in your IDE (VS Code / Cursor / Antigravity)
```bash
# Install extensions
ProfileName:"legacy-mssql"
Server:[IP_ADDRESS] #localhost
Database:master
Username:sa
Password:[PASSWORD] #FdeDeveloper12345678!

```

# Instructions for data ingestion on EC2 Instance

- Instance type: c7i-flex.large (free tier available)
- Storage: Minimum 30 GB
- Operating System: Ubuntu (linux)
- Security group > attach the security while creating ec2 instance
- SSH using .pem file from your system
- Install the docker

```bash
# Install the required packages
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Add the Docker repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker
```