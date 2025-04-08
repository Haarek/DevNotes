# 🧩 EF Core Task: Implement a Many-to-Many Relationship

## 🎯 Goal

In this task, you will implement a **many-to-many** relationship between `Order` and `Product`. This will help you understand how EF Core handles join tables and how to query complex relationships using LINQ.

---

## 🧠 Scenario

Each **Order** can contain multiple **Products**, and each **Product** can be part of many **Orders**.

You will create a **join entity** called `OrderProduct` that includes a `Quantity` field.

---

## 👣 Step-by-Step Instructions

### 1. Ensure the `Product` model exists

```csharp
public class Product
{
    public int Id { get; set; }
    public required string Name { get; set; }
    public decimal Price { get; set; }

    public ICollection<OrderProduct> OrderProducts { get; set; } = new List<OrderProduct>();
}
```

---

### 2. Create the join entity `OrderProduct`

```csharp
public class OrderProduct
{
    public int OrderId { get; set; }
    public Order Order { get; set; } = null!;

    public int ProductId { get; set; }
    public Product Product { get; set; } = null!;

    public int Quantity { get; set; }
}
```

---

### 3. Update the `Order` model

```csharp
public class Order
{
    public int Id { get; set; }
    public int CustomerId { get; set; }
    public Customer Customer { get; set; } = null!;

    public ICollection<OrderProduct> OrderProducts { get; set; } = new List<OrderProduct>();
}
```

---

### 4. Update `AppDbContext`

Add this DbSet:

```csharp
public DbSet<OrderProduct> OrderProducts => Set<OrderProduct>();
```

Then configure the relationship in `OnModelCreating`:

```csharp
modelBuilder.Entity<OrderProduct>()
    .HasKey(op => new { op.OrderId, op.ProductId });

modelBuilder.Entity<OrderProduct>()
    .HasOne(op => op.Order)
    .WithMany(o => o.OrderProducts)
    .HasForeignKey(op => op.OrderId);

modelBuilder.Entity<OrderProduct>()
    .HasOne(op => op.Product)
    .WithMany(p => p.OrderProducts)
    .HasForeignKey(op => op.ProductId);
```

---

### 5. Add a migration and update the database

```bash
dotnet ef migrations add AddOrderProductManyToMany
dotnet ef database update
```

---

### 6. Insert sample data

```csharp
var order = new Order { CustomerId = 1 };
order.OrderProducts.Add(new OrderProduct { ProductId = 1, Quantity = 2 });
order.OrderProducts.Add(new OrderProduct { ProductId = 2, Quantity = 1 });

context.Orders.Add(order);
context.SaveChanges();
```

---

### 7. Query data with LINQ

```csharp
var ordersWithProducts = context.Orders
    .Include(o => o.OrderProducts)
    .ThenInclude(op => op.Product)
    .ToList();

foreach (var o in ordersWithProducts)
{
    Console.WriteLine($"Order {o.Id}:");

    foreach (var op in o.OrderProducts)
    {
        Console.WriteLine($"  {op.Product.Name} x {op.Quantity}");
    }
}
```

---

## 🧪 Bonus Challenge

- Write a query to list all products and how many orders each appears in.
- Write a query to show the total price of each order.

---

Good luck and have fun exploring many-to-many relationships in EF Core!
