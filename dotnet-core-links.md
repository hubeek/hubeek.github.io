# Dotnet core links

_Status: Published_
_Created: 2018-11-22 02:08:33_
_Tags: mvc, .net, #c, dotnetcore, dotnet, mysql_

##Dotnet Identity & mySQL

[working identity with pomelo in dotnet 2.1](https://retifrav.github.io/blog/2018/03/20/csharp-dotnet-core-identity-mysql/)

[Nice article dotnet core 2 with link sql creation file](https://www.radenkozec.com/asp-net-identity-2-1-for-mysql/)

[identity proj](https://github.com/aspnet/Docs/blob/master/aspnet/identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)

[implementing Identity storage provider](https://docs.microsoft.com/en-us/aspnet/identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider)

```
UPDATE mysql.user SET Password=PASSWORD('root') WHERE User='root'; 

or

 ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
```

```
docker exec -i mysql-server mysql -uroot -p"root" mysql < orkestpit.sql
```

with homebew:
```
brew tap homebrew/services
brew services list
brew install mysql@5.7
brew services start mysql
mysql_secure_installation

echo 'export PATH="/usr/local/opt/mysql@5.7/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
mysql -V
```