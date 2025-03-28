# GCloud

_Status: Published_
_Created: 2020-01-13 14:38:16_
_Tags: cloud, dotnet core, express, node, docker_

## Dotnet core 2.2 project 


-  install [gcloud cli](https://cloud.google.com/sdk/gcloud/) installed
-  run gcloud ```auth configure-docker``` to setup gcloud 
-  [Google Run](https://cloud.google.com/run/ ) needs an image in the [Google Registry](https://cloud.google.com/container-registry/ )


In  Program.cs  
<code>
public static void Main(string[] args)
{
    CreateWebHostBuilder(args).UseUrls("http://*:8080/").Build().Run();
}
</code>
Dockerfile
<code>
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
ENV ASPNETCORE_URLS=http://*:${PORT} 
WORKDIR /app
COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "tuinhok.dll"]
</code>


.dockerignore
```
bin\
obj\
```


docker build and push
<code>
 docker build -t gcr.io/<gcp-project>/<appName>:latest .
 docker push gcr.io/<gcp-project>/<appName>:latest
</code>

## Node express server

```
const express = require('express')
const app = express()
const port = process.env.PORT || 8080

app.get('/', (req, res) => {
  res.json({
    message: 'Hello World'
  })
})

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

dockerfile for a node project:
```
FROM node:10

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm install

COPY . .
CMD ["node", "server-app.js"]
```
