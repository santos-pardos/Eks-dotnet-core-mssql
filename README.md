## Docker Hub
```
docker pull santospardos/sanvalero:docker-compose-dotnet-core-and-mssql-db
(1433)
docker pull santospardos/sanvalero:docker-compose-dotnet-core-and-mssql-app 
(80)
```
## DBeaver
```
docker run -d --name cloudbeaver --rm -ti -p 80:8978 -v /opt/cloudbeaver/workspace dbeaver/cloudbeaver:latest
```
## Docker MsSql
```
sudo docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong@Passw0rd>" \
   -p 1433:1433 --name sql1 --hostname sql1 \
   -d \
   mcr.microsoft.com/mssql/server:2022-latest
```
   
## RDS script
```
CREATE DATABASE [product-db]
GO

USE [product-db];
GO

CREATE TABLE product (
	Id INT NOT NULL IDENTITY,
	Name TEXT NOT NULL,
	Description TEXT NOT NULL,
	PRIMARY KEY (Id)
);
GO

INSERT INTO [product] (Name, Description)
VALUES 
('Dependency Injection Principles, Practices, and Patterns', 'Book by Steven van Deursen and Mark Seemann'),
('Agile Software Development, Principles, Patterns, and Practices', 'Book by Robert C. Martin'); 
GO
```

## Docker compose Dotnet Core and Microsoft SQL Server example system 

Example docker-compose system, based on .NET Core project and Microsoft SQL Server database (accessed with _Dapper_).

Dotnet Dockerfile and basic Docker setup based on [SoftwareDeveloper.Blog introduction to _Docker_](https://www.softwaredeveloper.blog/multi-project-dotnet-core-solution-in-docker-image) and database initialization based on [SoftwareDeveloper.Blog introduction to MS SQL Server initialized in _Docker_ container](https://www.softwaredeveloper.blog/initialize-mssql-in-docker-container).

## Docker-compose up
if you want to see this example running, you can just type `docker-compose up` from solution directory.

## Docker-compose up -d
If you want run this example but without attaching console, run _docker-compose up_ in detach mode - `docker-compose up -d`.

## Docker-compose up --build
If you have already composed system up, but then changed source code, you need to pass _--build_ parameter, when running _docker-compose up_ next time: `docker-compose up --build`.
Of course it can be used along with detach parameter.

## Docker-compose down
When you want to clean up containers and networks created by _docker-compose_, just type `docker-compose down` from solution directory.

## Check if system works
If you want to see if this example system works properly, just access in your browser following GET address - `http://localhost:8080` and you should see following results taken from database:

``` json
[
  {
    "id": 1,
    "name": "Dependency Injection Principles, Practices, and Patterns",
    "description": "Book by Steven van Deursen and Mark Seemann"
  },
  {
    "id": 2,
    "name": "Agile Software Development, Principles, Patterns, and Practices",
    "description": "Book by Robert C. Martin"
  }
]
```
Remember to wait 90 seconds to have DB initialized, due to [the recommended way MS _SQL Server_ need to be initialized](https://www.softwaredeveloper.blog/initialize-mssql-in-docker-container).
If you know that your PC will boot up _SQL Server_ faster than 90 seconds you can decrease this time in _run-initialization.sh_ script.
