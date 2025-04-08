# Entity Framework Core Workshop
  
Welcome to the EF Core Workshop! This guide will walk you through setting up a small database-driven app using Entity Framework Core in a .NET console application.

## 🧠 What is an ORM and Why Use Entity Framework Core?

In software development, we often need to store and retrieve data from a database. Instead of writing raw SQL queries everywhere in our code, we can use an **Object-Relational Mapper (ORM)**.

An **ORM** helps bridge the gap between:
- 🧱 **Relational Databases** (like SQL Server)
- 💻 **Object-Oriented Code** (like your C# classes)

Entity Framework Core (EF Core) is Microsoft’s modern, lightweight ORM for .NET. It allows you to:
- Define your database schema using **C# classes**
- Use **LINQ** to query data
- **Migrate** schema changes without manual SQL
- Work across many database systems (SQL Server, SQLite, PostgreSQL, etc.)

With EF Core, your data logic is centralized, strongly typed, and easier to maintain.

### Topics in this workshop

- Model entities with relationships
- Connect to SQL Server
- Create and apply migrations
- Seed and query data effectively
- Use LINQ for data access
- Perform CRUD operations
- Handle relationships (one-to-many, many-to-many)
  
---

## 🚀 Setup Instructions

### Requirements

- tested on .net 9.0.3
- Visual Studio 2022 or vscode
- Workshop sql server instance (or local SQL Server Express)
- SQL Server Management Studio (SSMS) or Azure Data Studio
- dotnet CLI installed
- EF Core CLI tools installed
- SQL Server Management Studio (SSMS) or Azure Data Studio
- Visual Studio Code (optional)

### 1. Create a new console app

Add a unique name for your app:

```bash
dotnet new console -n EfDemoApp
cd EfDemoApp
```

### 2. Add NuGet packages

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer

dotnet add package Microsoft.EntityFrameworkCore.Design

dotnet add package Microsoft.Extensions.Configuration

dotnet add package Microsoft.Extensions.Configuration.Json

dotnet add package Microsoft.Extensions.Configuration.FileExtensions
```

### 3. Add `appsettings.json` 

Add the file to the root of the project directory. This file will hold your connection string and other configuration settings.

Configure your connection string in `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=EfDemoDb;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
```

> 📌 Right-click the file in VS and set **Copy to Output Directory**: *Copy if newer*

---

## 🧱 Define Your Models

Create a `Models` folder and add three classes:

### Customer.cs

```csharp
public class Customer
{
    public int Id { get; set; }
    public required string Name { get; set; }
    public ICollection<Order> Orders { get; set; } = new List<Order>();
}
```

### Order.cs

```csharp
public class Order
{
    public int Id { get; set; }
    public int CustomerId { get; set; }
    public Customer Customer { get; set; } = null!;
    public ICollection<OrderLine> OrderLines { get; set; } = new List<OrderLine>();
}
```

### OrderLine.cs

```csharp
public class OrderLine
{
    public int Id { get; set; }
    public int OrderId { get; set; }
    public required string ProductName { get; set; }
    public int Quantity { get; set; }
    public decimal Price { get; set; }
    public Order Order { get; set; } = null!;
}
```

---

## 🔧 Create AppDbContext

Add a `Data` folder and create `AppDbContext.cs`:

```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }

    public DbSet<Customer> Customers => Set<Customer>();
    public DbSet<Order> Orders => Set<Order>();
    public DbSet<OrderLine> OrderLines => Set<OrderLine>();

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        modelBuilder.Entity<Customer>().HasData(
            new Customer { Id = 1, Name = "Alice" },
            new Customer { Id = 2, Name = "Bob" }
        );

        modelBuilder.Entity<Order>().HasData(
            new Order { Id = 1, CustomerId = 1 },
            new Order { Id = 2, CustomerId = 2 }
        );

        modelBuilder.Entity<OrderLine>().HasData(
            new OrderLine { Id = 1, OrderId = 1, ProductName = "Apples", Quantity = 2, Price = 10.5m },
            new OrderLine { Id = 2, OrderId = 2, ProductName = "Bananas", Quantity = 5, Price = 3.2m }
        );
    }
}
```

Also add the AppDbContextFactory class to help with migrations in the `Data` folder.

### AppDbContextFactory.cs

```csharp
public class AppDbContextFactory : IDesignTimeDbContextFactory<AppDbContext>
{
    public AppDbContext CreateDbContext(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("appsettings.json")
            .Build();

        var optionsBuilder = new DbContextOptionsBuilder<AppDbContext>();
        optionsBuilder.UseSqlServer(config.GetConnectionString("DefaultConnection"));

        return new AppDbContext(optionsBuilder.Options);
    }
}
```

---

## 🛠 Create and Apply Migration

```bash
dotnet ef migrations add InitialCreate

dotnet ef database update
```

---

## 🧪 Test the Context in `Program.cs`

```csharp
using EfDemoApp.Data;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;

var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appsettings.json")
    .Build();

var connectionString = config.GetConnectionString("DefaultConnection");
var options = new DbContextOptionsBuilder<AppDbContext>()
    .UseSqlServer(connectionString)
    .Options;

using var context = new AppDbContext(options);
{
    Console.WriteLine($"Customers: {context.Customers.Count()}");
    Console.WriteLine($"Orders: {context.Orders.Count()}");
    Console.WriteLine($"OrderLines: {context.OrderLines.Count()}");
}
```

---

## 🎓 Student Tasks

1. **Add a phone number to Customer**

   - Modify the model
   - Create a new migration
   - Update the database

2. **Add a new table: Product**

   - Fields: `Id`, `Name`, `Price`
   - Link `OrderLine` to `Product` (one-to-many)
   - Seed a few products

3. **Write code to insert new Customers, Orders, OrderLines, and Products**

4. **Query data using LINQ**

   - Get all orders with customer names and order totals
   - Group orders by customer
   - Use joins and projections
  
5. **Add a many-to-many relationship**

   - Create a new `OrderProduct` entity to link `Order` and `Product`
   - Update the models and context
   - Seed data for this relationship
   - Write LINQ queries to retrieve orders with products
   - [Instructions for many-to-many](WorkShop/task-many-to-many.md)

---

## 📎 Resources

- [LINQ Cheat Sheet](../docs/linq-cheatsheet.md)
- [EF Core Docs](https://learn.microsoft.com/en-us/ef/core/)
- [dotnet ef CLI Reference](https://learn.microsoft.com/en-us/ef/core/cli/dotnet)

---

Happy coding! 🎉

