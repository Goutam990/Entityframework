# Entitity framework

![Entity Framework Diagram](https://github.com/Goutam990/Entityframework/blob/master/intity_framework.png?raw=true)

## intitity framework (ASP.NET Core MVC + EF Core)

A minimal ASP.NET Core MVC app using Entity Framework Core (SQL Server) with a simple `Product` entity and a page to list and create products.

### Requirements
- **.NET SDK 8.x** (works with 9.x runtime too)
- **SQL Server** (SQL Express or LocalDB)
- Windows PowerShell/Terminal

### Project Structure
- `intitity framework.csproj` – main web project
- `Controllers/ProductsController.cs` – list/create actions
- `Models/Product.cs` – entity
- `Models/ApplicationDbContext.cs` – EF Core `DbContext`
- `Views/Products/Index.cshtml` – UI to list and create products
- `appsettings.json` – connection string

### Setup
1) Restore and build
```bash
cd "intitity framework"
dotnet restore
dotnet build
```

2) Configure the database in `appsettings.json`
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=HOMEPAGE-LP-18\\SQLEXPRESS;Database=ApplicationDbContext;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true"
  }
}
```
- For LocalDB use: `Server=(localdb)\\MSSQLLocalDB;Database=ApplicationDbContext;Trusted_Connection=True;MultipleActiveResultSets=true`

3) Run the app
```bash
dotnet run --project ".\intitity framework\intitity framework.csproj"
```
Launch URLs (from `launchSettings.json`):
- HTTP: `http://localhost:5203`
- HTTPS: `https://localhost:7000`

4) Use Products page
- Navigate to `http://localhost:5203/Products` to view and add products.

### Database Initialization
For developer convenience, the app calls `Database.EnsureCreated()` on startup to auto-create the schema if needed. If you prefer migrations instead:
```bash
# Install EF CLI matching EF 8.x
 dotnet tool install -g dotnet-ef --version 8.0.8

# From project directory
 cd "intitity framework"
 dotnet ef migrations add InitialCreate -o Migrations
 dotnet ef database update
```
Then remove the `EnsureCreated()` block in `Program.cs`.

### Useful Commands
```bash
# Build & run
 dotnet build
 dotnet run --project ".\intitity framework\intitity framework.csproj"

# Clean
 dotnet clean

# Restore
 dotnet restore
```

### Troubleshooting
- **MSB3021 file in use**: Stop the running app, then clean/build.
```powershell
Get-Process | Where-Object { $_.Path -like '*intitity framework.exe' } | Stop-Process -Force
```
- **SQL SSL trust error**: Add `TrustServerCertificate=True` to the connection string (dev only) or install a trusted certificate.
- **Decimal precision warning**: `Price` uses `decimal(18,2)`. Adjust via Fluent API if your domain needs different precision.

### License
For learning/demo purposes.
