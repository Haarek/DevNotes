# 🗂 EF Core Cue Cards for Live Demo

Use these cue cards to guide your live Entity Framework Core demo in Visual Studio. Each card is a teaching checkpoint with a short explanation or prompt.

---

## 🎬 Cue Card 1: What is EF Core?

- EF Core is an ORM that lets us work with databases using C# classes.
- It maps tables to classes, rows to objects.
- It removes the need for most raw SQL in app code.

---

## 🧱 Cue Card 2: The Data Model (ER to Classes)

- Show the ER diagram: Customer → Order → OrderLine
  ![ER Diagram](../assets/images/erdiagram.png)

- Walk through the three entity classes
- Explain navigation properties and collections

---

## 🧰 Cue Card 3: Setting up EF Core in a Console App

- Show `Program.cs`, `appsettings.json`, and the NuGet packages
- Point out `DbContextOptionsBuilder`
- Explain what `OnConfiguring` vs injected options means

---

## 🧑‍🍳 Cue Card 4: Creating `AppDbContext`

- Show the `AppDbContext` class
- Point out `DbSet<T>` properties
- Explain what `DbContext` does behind the scenes
- Mention lifecycle (injected/disposed)

---

## 🧪 Cue Card 5: Adding a Migration

- Run: `dotnet ef migrations add InitialCreate`
- Show what files get generated
- Explain how migrations track schema changes in code

---

## 🗃 Cue Card 6: Applying the Migration

- Run: `dotnet ef database update`
- Open SQL Server and show the created tables
- Optionally show raw data

---

## 🌱 Cue Card 7: Seeding Data

- Show how seeding works in `OnModelCreating`
- Mention primary key requirements for seeding
- Run `dotnet ef migrations add SeedData` if applicable

---

## 🔍 Cue Card 8: Querying with LINQ

- Query Customers and Orders in `Program.cs`
- Show `.Include(...)` to eager-load navigation properties
- Use projection to flatten results

---

## 🧩 Cue Card 9: Many-to-Many Relationships

- Introduce `OrderProduct` join table
- Show how to configure composite key in Fluent API
- Demo inserting and querying many-to-many data

---

## 🛠 Cue Card 10: Common Student Tasks

- Add a new property (e.g., Phone on Customer)
- Add a new entity (Product)
- Add insert and query code
- Encourage exploration with LINQ

---

## 📎 Cue Card 11: Key Takeaways

- EF Core is powerful, but transparent — your C# shapes the DB
- Migrations let you evolve the schema safely
- LINQ makes querying expressive and type-safe

---

End with questions or hands-on coding time 🎉
