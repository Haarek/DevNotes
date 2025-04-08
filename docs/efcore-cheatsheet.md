# Entity Framework Core Command Cheat Sheet

This cheat sheet lists the most common EF Core commands using both the **Package Manager Console (PMC)** and the **`dotnet ef` CLI**.

## Common EF Core Commands

| Task                                | PMC Command                                         | `dotnet ef` CLI Command                                      |
|-------------------------------------|-----------------------------------------------------|---------------------------------------------------------------|
| **Add a migration**                 | `Add-Migration MigrationName`                      | `dotnet ef migrations add MigrationName`                     |
| **Remove last migration**           | `Remove-Migration`                                 | `dotnet ef migrations remove`                                |
| **Update database**                 | `Update-Database`                                  | `dotnet ef database update`                                  |
| **Update to specific migration**    | `Update-Database MigrationName`                    | `dotnet ef database update MigrationName`                    |
| **Drop the database**               | `Drop-Database`                                    | `dotnet ef database drop`                                    |
| **List migrations**                 | `Get-Migrations`                                   | `dotnet ef migrations list`                                  |
| **Apply pending migrations**        | _(PMC uses `Update-Database`)_                      | `dotnet ef database update`                                  |
| **Generate SQL script**             | `Script-Migration`                                 | `dotnet ef migrations script`                                |
| **Script to a specific migration**  | `Script-Migration From To`                         | `dotnet ef migrations script FromMigration ToMigration`       |
| **Reverse engineer (Scaffold)**     | `Scaffold-DbContext`                               | `dotnet ef dbcontext scaffold`                               |
| **Get database info**               | _N/A_                                              | `dotnet ef dbcontext info`                                   |
| **List DbSets in context**          | _N/A_                                              | `dotnet ef dbcontext list`                                   |
| **Get context's connection string** | _N/A_                                              | `dotnet ef dbcontext info` (includes this info)              |

## Pro Tips

- `dotnet ef` must be run from the project folder, or use `--project` and `--startup-project` to specify paths.
- Reverse engineering example:
  ```bash
  dotnet ef dbcontext scaffold "your_connection_string" Microsoft.EntityFrameworkCore.SqlServer -o Models
  ```
