# .net core connect local mysql

_Status: Published_
_Created: 2018-10-06 05:31:37_
_Tags: dotnet .net_

choose mysql
local with mamp or docker
---
install
nuget
Pomelo.EntityFrameworkCore.MySql
---
in appsettings.json:

<code>
 "ConnectionStrings": {
    "DefaultConnection": "server=localhost;port=3306;database=dotnetmysqltest;uid=username;password=password",
  }
</code>

setup entities
recipe.class
<code>
using System;
using System.Collections.Generic;

namespace testlocalmysql.Entities
{
    public class Recipe
    {
       
        public int RecipeId { get; set; }
        public string Name { get; set; }
       // public TimeSpan TimeToCook { get; set; } // gave error time(6) ???
// works as double
        public double TimeToCook { get; set; }
        public bool IsDeleted { get; set; }
        public string Method { get; set; }

        public ICollection<Ingredient> Ingredients { get; set; }
    }
}

</code>
ingredient.class
<code>
using System;
namespace testlocalmysql.Entities
{
    public class Ingredient
    {
        public int IngredientId { get; set; }
        public int RecipeId { get; set; }
        public string Name { get; set; }
        public decimal Quantity { get; set; }
        public string Unit { get; set; }
    }
}
</code>

register dbcontext
<code>
using System;
using Microsoft.EntityFrameworkCore;
using testlocalmysql.Entities;

namespace testlocalmysql.Db
{
    public class AppDbContext: DbContext
    {
        public AppDbContext(DbContextOptions<AppDbContext> options) : base(options)
        {
        
        }
            
        public DbSet<Recipe> Recipes { get; set; }

    }
}
</code>
add to startup.cs
<code>

            services.AddDbContext<AppDbContext>(options =>
            options.UseMySql(Configuration.GetConnectionString("DefaultConnection")));
</code>


use ef
test if works
<code>
 dotnet ef --help
</code>
apply first migration
<code>
dotnet ef migrations add InitialSchema
</code>
migration folder is created with 3 new files
finish it with
<code>
dotnet ef database update
</code>