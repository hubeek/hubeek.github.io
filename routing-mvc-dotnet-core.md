# Routing mvc dotnet core

_Status: Published_
_Created: 2018-10-06 14:46:12_
_Tags: dotnet .net_

In startup.cs
<code>
app.UseMvc(routes =>
{
    //New Route
    routes.MapRoute(
       name: "about-route",
       template: "about",
       defaults: new { controller = "Home", action = "About" }
    );
 
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});
</code>
with attributes
<code>
[Route("[controller]")]
public class AnalyticsController : Controller
{
    [Route("Dashboard")]
    public IActionResult Index()
    {
        return View();
    }
 
    [Route("[action]")]
    public IActionResult Charts()
    {
        return View();
    }
}
</code>
rest
<code>
[Route("api/[controller]")]
public class ValuesController : Controller
{
    // GET api/values
    [HttpGet]
    public IEnumerable<string> Get()
    {
        return new string[] {"hello", "world!"};
    }
 
    // POST api/values
    [HttpPost]
    public void PostCreate([FromBody] string value)
    {
    }
}
</code>
constraints
<code>
[HttpGet("{id:int}")]
public string GetById(int id)
{
    return "item " + id;
}
</code>