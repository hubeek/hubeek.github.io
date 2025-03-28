# MSSQL server with Docker

_Status: Published_
_Created: 2019-01-04 15:19:22_
_Tags: docker, mssql, dotnet, .net_

https://database.guide/how-to-install-sql-server-on-a-mac/

get docker container
<code>
sudo docker pull microsoft/mssql-server-linux:latest
</code>
create docker container
password needs 
Uppercase letters, Lowercase letters, Base 10 digits, and Symbols..
<code>
docker run -e'ACCEPT_EULA=Y' -e'MSSQL_SA_PASSWORD=YourPassword123!' -p 1433:1433 --name sqlserver -d microsoft/mssql-server-linux
</code>
start docker container
<code>
docker exec -it sqlserver bash
</code>
run as SA
<code>
/opt/mssql-tools/bin/sqlcmd -U SA
</code>
view password (!)
<code>
echo $MSSQL_SA_PASSWORD
</code>
change password:
<code>
docker exec -it sqlserver2 /opt/mssql-tools/bin/sqlcmd -U SA'Root123!' -Q'ALTER LOGIN SA WITH PASSWORD="YourPassword123!"'
</code>
download
<a href="https://docs.microsoft.com/en-us/sql/azure-data-studio/download?view=sql-server-2017">mssql datastudio</a>

create and save data  in volume
<code>
docker run -e'ACCEPT_EULA=Y' -e'MSSQL_SA_PASSWORD=YourPassword123!' -p 1433:1433 --name sqlserver2 -v sqlservervolume:/var/opt/mssql -d microsoft/mssql-server-linux
</code>
to see volumes
<code>
docker volume ls
</code>
backup external to local desktop...
<code>
docker cp newsqlserver:/var/opt/mssql ~/Desktop
</code>
copy into container
<code>
docker cp ~/Desktop/filetocopy.ext newsqlserver:/
</code>
backup from within the mssql in new backup folder
<code>
/opt/mssql-tools/bin/sqlcmd -U SA //get in db
1> BACKUP DATABASE Products TO DISK ='/var/opt/mssql/backup/Products.bak'
2> GO
</code>
exit 
copy it to desired location...

code first approach:
dotnet ef migrations add InitialMigration
dotnet ef database update

sql operations studio:
no longer in active development...

azure datastudio:
same as sql operations studio...
https://docs.microsoft.com/en-us/sql/azure-data-studio/download?view=sql-server-2017

in azure datastudio:
new query
<code>
IF NOT EXISTS (
   SELECT name
   FROM sys.databases
   WHERE name = N'TutorialDB'
)
CREATE DATABASE [TutorialDB]
GO

ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
GO
</code>
