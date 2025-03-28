# Upload with form

_Status: Published_
_Created: 2018-10-07 09:31:42_
_Tags: dotnet .net_

model
<code>
 public class ProductEditModel
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public decimal Rate { get; set; }
        public int Rating { get; set; }
    }
</code>
controller
<code>
[HttpGet]
        public IActionResult Create()
        {
            return View();
        }


        [HttpPost]
        public IActionResult Create(ProductEditModel model)
        {
            string message = "";

            if (ModelState.IsValid)
            {
                message = "product " + model.Name + " Rate " + model.Rate.ToString() + " With Rating " + model.Rating.ToString() + " created successfully";
                ProductEditModel p = new ProductEditModel();
                p.Name = model.Name;
                p.Rate = model.Rate;
                p.Rating = model.Rating;
                ViewData["product"] = p;
                ViewData["isSuccess"] = true;

            }
            else
            {
                ViewData["isError"] = true;
                message = "Failed to create the product. Please try again";
            }
            ViewData["Message"] = message;
            return View();
        }
</code>
razor
<code>
@{
    ViewData["Title"] = "Bla Create";
    var product = ViewData["Product"] as ProductEditModel;
    var isSuccess = ViewData["isSuccess"] as Boolean?;
    var isError = ViewData["isError"] as Boolean?;
}

<h2>Create</h2>
@if (@isSuccess == true)
{

    <div class="alert alert-success" role="alert">
        @ViewData["Message"]
    </div>
}
@if (@isError == true)
{

    <div class="alert alert-danger" role="alert">
        @ViewData["Message"]
    </div>
}

@if (@product != null)
{
    <p>
        <a asp-area="" asp-controller="Bla" asp-action="Create">Create</a>
        <a asp-area="" asp-controller="Bla" asp-action="Index">Bla</a>
    </p>

}
else
{
    <form action="/bla/create" method="post">
        <label for="Name">Name</label>
        <input type="text" name="Name" />

        <label for="Rate">Rate</label>
        <input type="text" name="Rate" />
        <label for="Rating">Rating</label>
        <input type="text" name="Rating" />
        <input type="submit" name="submit" />
    </form>
}

</code>