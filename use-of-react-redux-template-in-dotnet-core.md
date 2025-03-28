# Use of React Redux Template in dotnet core

_Status: Published_
_Created: 2018-11-08 02:18:36_
_Tags: dotnet .net dotnetcore react redux_

<code>
hjh /D/t/Dotnet> mkdir reactnativedotnettest
hjh /D/t/Dotnet> cd reactnativedotnettest/
hjh /D/t/D/reactnativedotnettest> dotnet new reactredux

Welcome to .NET Core!
---------------------
Learn more about .NET Core: https://aka.ms/dotnet-docs
Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli-docs

Telemetry
---------
The .NET Core tools collect usage data in order to help us improve your experience. The data is anonymous and doesn't include command-line arguments. The data is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET Core CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry

ASP.NET Core
------------
Successfully installed the ASP.NET Core HTTPS Development Certificate.
To trust the certificate run 'dotnet dev-certs https --trust' (Windows and macOS only). For establishing trust on other platforms refer to the platform specific documentation.
For more information on configuring HTTPS see https://go.microsoft.com/fwlink/?linkid=848054.
Getting ready...
The template "ASP.NET Core with React.js and Redux" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on /Development/tmp/Dotnet/reactnativedotnettest/reactnativedotnettest.csproj...
  Restoring packages for /Development/tmp/Dotnet/reactnativedotnettest/reactnativedotnettest.csproj...
  Generating MSBuild file /Development/tmp/Dotnet/reactnativedotnettest/obj/reactnativedotnettest.csproj.nuget.g.props.
  Generating MSBuild file /Development/tmp/Dotnet/reactnativedotnettest/obj/reactnativedotnettest.csproj.nuget.g.targets.
  Restore completed in 7.45 sec for /Development/tmp/Dotnet/reactnativedotnettest/reactnativedotnettest.csproj.

Restore succeeded.

hjh /D/t/D/reactnativedotnettest> ll
total 48
drwxr-xr-x  13 hjhubeek  wheel   442B Nov  8 08:14 .
drwxr-xr-x   4 hjhubeek  wheel   136B Nov  8 08:13 ..
-rw-r--r--   1 hjhubeek  wheel   3.7K Nov  8 08:14 .gitignore
drwxr-xr-x   8 hjhubeek  wheel   272B Nov  8 08:14 ClientApp
drwxr-xr-x   3 hjhubeek  wheel   102B Nov  8 08:14 Controllers
drwxr-xr-x   5 hjhubeek  wheel   170B Nov  8 08:14 Pages
-rw-r--r--   1 hjhubeek  wheel   640B Nov  8 08:14 Program.cs
drwxr-xr-x   3 hjhubeek  wheel   102B Nov  8 08:14 Properties
-rw-r--r--   1 hjhubeek  wheel   2.1K Nov  8 08:14 Startup.cs
-rw-r--r--   1 hjhubeek  wheel   146B Nov  8 08:14 appsettings.Development.json
-rw-r--r--   1 hjhubeek  wheel   105B Nov  8 08:14 appsettings.json
drwxr-xr-x   6 hjhubeek  wheel   204B Nov  8 08:14 obj
-rw-r--r--   1 hjhubeek  wheel   2.3K Nov  8 08:14 reactnativedotnettest.csproj
hjh /D/t/D/reactnativedotnettest> cd ClientApp/
hjh /D/t/D/r/ClientApp> npm install

> uglifyjs-webpack-plugin@0.4.6 postinstall /Development/tmp/Dotnet/reactnativedotnettest/ClientApp/node_modules/uglifyjs-webpack-plugin
> node lib/post_install.js

added 1183 packages from 756 contributors and audited 10649 packages in 24.888s
found 341 vulnerabilities (313 low, 15 moderate, 12 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details
hjh /D/t/D/r/ClientApp> dotnet restore
MSBUILD : error MSB1003: Specify a project or solution file. The current working directory does not contain a project or solution file.
hjh /D/t/D/r/ClientApp> ll  //// Oops wrong folder... better go one folder up
total 944
drwxr-xr-x    9 hjhubeek  wheel   306B Nov  8 08:15 .
drwxr-xr-x   13 hjhubeek  wheel   442B Nov  8 08:14 ..
-rw-r--r--    1 hjhubeek  wheel   306B Nov  8 08:14 .gitignore
-rw-r--r--    1 hjhubeek  wheel   109K Nov  8 08:14 README.md
drwxr-xr-x  918 hjhubeek  wheel    30K Nov  8 08:15 node_modules
-rw-r--r--    1 hjhubeek  wheel   350K Nov  8 08:15 package-lock.json
-rw-r--r--    1 hjhubeek  wheel   687B Nov  8 08:14 package.json
drwxr-xr-x    5 hjhubeek  wheel   170B Nov  8 08:14 public
drwxr-xr-x    9 hjhubeek  wheel   306B Nov  8 08:14 src
hjh /D/t/D/r/ClientApp> cd ..
hjh /D/t/D/reactnativedotnettest> dotnet restore
  Restore completed in 51.8 ms for /Development/tmp/Dotnet/reactnativedotnettest/reactnativedotnettest.csproj.
hjh /D/t/D/reactnativedotnettest> dotnet run
Using launch settings from /Development/tmp/Dotnet/reactnativedotnettest/Properties/launchSettings.json...
: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using '/Users/hjhubeek/.aspnet/DataProtection-Keys' as key repository; keys will not be encrypted at rest.
info: Microsoft.AspNetCore.SpaServices[0]
      Starting create-react-app server on port 49656...
Hosting environment: Development
Content root path: /Development/tmp/Dotnet/reactnativedotnettest
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
info: Microsoft.AspNetCore.SpaServices[0]
      > reactnativedotnettest@0.1.0 start /Development/tmp/Dotnet/reactnativedotnettest/ClientApp
      > rimraf ./build && react-scripts start
      
      Starting the development server...
      
info: Microsoft.AspNetCore.SpaServices[0]
      
      Compiled successfully!
      
info: Microsoft.AspNetCore.SpaServices[0]
      You can now view reactnativedotnettest in the browser.
      
info: Microsoft.AspNetCore.SpaServices[0]
        Local:            http://localhost:49656/
        On Your Network:  http://xx.xx.xx.xx:49656/
      

</code>

<h2>Side Note</h2>
Duplicate files are shown in visual studio...
