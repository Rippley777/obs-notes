1. **Define a model class:** First, create a simple model class to represent the data you want to return as JSON. For example, create a `Person` class:

    
    `namespace MyBackend.Models {     public class Person     {         public string Name { get; set; }         public int Age { get; set; }     } }`
    
2. **Add a new action method to your controller:** In your `SampleController` (or any other controller), add a new action method that returns an instance of the `Person` class:
    
    `using Microsoft.AspNetCore.Mvc; using MyBackend.Models;  namespace MyBackend.Controllers {     [ApiController]     [Route("[controller]")]     public class SampleController : ControllerBase     {         [HttpGet]         public IActionResult Get()         {             return Ok("Hello from .NET Core Web API");         }          [HttpGet("person")]         public IActionResult GetPerson()         {             var person = new Person             {                 Name = "John Doe",                 Age = 30             };              return Ok(person);         }     } }`
    
    In this example, the `GetPerson` method creates a new instance of the `Person` class and returns it as JSON. The `[HttpGet("person")]` attribute specifies that this action method is accessible via the `/sample/person` endpoint with a GET request.
    
3. **Run your application:** Start your .NET Core Web API and navigate to `http://localhost:5000/sample/person` in your browser or use a tool like Postman to send a GET request to this endpoint. You should see the JSON representation of the `Person` object:
    
    `{     "name": "John Doe",     "age": 30 }`
    

Now you have an endpoint in your .NET Core Web API that returns a JSON object. You can modify the `Person` class and the `GetPerson` method to return any data you need.


### Step 3: Register Controllers in Program.cs

In your `Program.cs` file, ensure that you have the following line in the `builder.Services` section to add controllers to the DI container:

csharp

Copy code

`builder.Services.AddControllers();`

And in the `app` section, ensure you have the following line to map controllers:

csharp

Copy code

`app.MapControllers();`

### Step 4: Build and Run the Application

Build your application to make sure there are no compilation errors:

bash

Copy code

`dotnet build`

Then, run your application:

bash

Copy code

`dotnet run`