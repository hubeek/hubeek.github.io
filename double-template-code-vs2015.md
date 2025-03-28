# double template code vs2015

_Status: Published_
_Created: 2019-06-27 12:44:00_
_Tags: .net, dotnet_

change in solution file (.csproj)
<code>
    <ItemGroup>
        <None Remove="$(SpaRoot)**" />
        <None Include="$(SpaRoot)**" Exclude="$(SpaRoot)node_modules\**" />
    </ItemGroup>
</code>