
# ConnectionStrings in ASP.NET Core

**1. Add the Connection String in appsettings.json**

```bash
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=your_server_name;Database=your_database_name;User Id=your_username;Password=your_password;"
  }
}
```
**2. Access the Connection String in Code**

In Program.cs:
Access the connection string using the Configuration object.

```bash
var builder = WebApplication.CreateBuilder(args);

// Access the connection string
var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");

builder.Services.AddDbContext<MyDbContext>(options =>
    options.UseSqlServer(connectionString));

var app = builder.Build();

```

**In Controllers or Services:**

Inject the ``IConfiguration`` service to retrieve the connection string.

```bash
public class MyService
{
    private readonly string _connectionString;

    public MyService(IConfiguration configuration)
    {
        _connectionString = configuration.GetConnectionString("DefaultConnection");
    }

    public void ConnectToDatabase()
    {
        Console.WriteLine($"Using connection string: {_connectionString}");
    }
}

```
