# dotnet core notes

_Status: Published_
_Created: 2019-09-14 04:26:34_
_Tags: dotnet, .net, scaffold, mysql_

localize date time
<code>
CultureInfo ci = new CultureInfo("nl-NL");
Console.WriteLine(DateTime.Now.ToString("D", ci));
</code>

scaffold mysql db
<code>
dotnet ef dbcontext scaffold "server=localhost;port=3306;user=root;password=root;database=opit" MySql.Data.EntityFrameworkCore -o Models -f
</code>