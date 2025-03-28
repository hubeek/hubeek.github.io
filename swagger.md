# swagger

_Status: Published_
_Created: 2019-12-16 16:41:54_
_Tags: dotnet, .net, dotnetcore, swagger_

add package:
NSwag.AspNetCore 

startup.cs
<code>
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();
    services.AddOpenApiDocument();
}

</code>
Configure(IApplicationBuilder app, IWebHostEnvironment env)
<code>
...(after endpoints)...
app.UseOpenApi();
app.UseSwaggerUi3();
</code>
goto url localhost:5000/swagger