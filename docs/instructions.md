# Ingesting data

- Download the dataset from "data\source\data.txt"
- Create a EC2 Instance with Ubuntu OS and Amazon Linux 2. 
- Configure the instance security group and assign a Elastic IP.
- Install Docker on the EC2 instance. 
- Docker Container > mcr.microsoft.com/mssql/server:2022-latest

```
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=FdeEnterprise12345678!" -p 1433:1433 --name legacy-mssql -d mcr.microsoft.com/mssql/server:2022-latest

# or multi-line in windows 
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=FdeEnterprise12345678!" ^
   -p 1433:1433 --name legacy-mssql ^
   -d mcr.microsoft.com/mssql/server:2022-latest

# or multi-line unix
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=FdeEnterprise12345678!" \
   -p 1433:1433 --name legacy-mssql \
   -d mcr.microsoft.com/mssql/server:2022-latest

# or multi-line with volume inside EC2
docker run -v mssql_data:/var/opt/mssql \
  -e "ACCEPT_EULA=Y" \
  -e "MSSQL_SA_PASSWORD=FdeEnterprise12345678!" \
  -p 1433:1433 \
  --name legacy-mssql \
  -d mcr.microsoft.com/mssql/server:2022-latest

```


- install the req > pip install -r requirements.txt

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
