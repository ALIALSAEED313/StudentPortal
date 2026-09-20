# StudentPortal

StudentPortal is a simple ASP.NET Core web application (Razor / MVC views) for managing students. It provides CRUD operations for student records and a clean responsive UI built with Bootstrap 5.

## Prerequisites

- .NET 10 SDK
- Visual Studio 2026 (or VS Code + C# extension)
- SQL Server / LocalDB (or other database supported by EF Core)
- (Optional) dotnet-ef tool: `dotnet tool install --global dotnet-ef`

## Project structure

- StudentPortal.slnx — Solution file
- StudentPortal.Web — Web project (contains Controllers, Views, Data, Models)

> Note: Views were updated to a modern Bootstrap 5 layout. Ensure Bootstrap and icons are available in the layout (_Layout.cshtml).

## Quick start (CLI)

1. Open a PowerShell terminal at the solution root:

   cd "C:\Users\aalsaeed.trainee.trainee\Desktop\tutorial project\MVC CRUD\StudentPortal"

2. Restore and build:

   dotnet restore
   dotnet build

3. Configure the database connection string in StudentPortal.Web/appsettings.json (or your environment secrets).

4. If migrations are used, create/apply them from the web project folder:

   cd StudentPortal.Web
   dotnet ef migrations add InitialCreate
   dotnet ef database update

5. Run the app:

   dotnet run

6. Open a browser and navigate to the URL shown in the console (typically https://localhost:5001).

## Using Visual Studio

- Open `StudentPortal.slnx` in Visual Studio 2026.
- Set `StudentPortal.Web` as the startup project.
- Update the connection string in appsettings.json or user secrets.
- Build and press F5 to run.

## Notes and troubleshooting

- If pages look broken, ensure Bootstrap 5 and Bootstrap Icons (or Font Awesome) are referenced in `_Layout.cshtml` or the site bundle.
- The Student entity property name was updated to follow EF conventions (Id). If you have an existing database, update migrations or adjust the schema accordingly.
- The controller actions use antiforgery tokens for POST actions. Ensure forms include `@Html.AntiForgeryToken()` (Razor helpers in views). For AJAX, include the antiforgery token in headers.

## Files of interest

- StudentPortal.Web/Controllers/StudentsController.cs
- StudentPortal.Web/Data/ApplicationDbContext.cs
- StudentPortal.Web/Models/Entities/Student.cs
- StudentPortal.Web/Views/Home/Index.cshtml
- StudentPortal.Web/Views/Home/Privacy.cshtml

## Contributing

Make changes on feature branches and open pull requests. Keep backend code unchanged unless you understand the data model and migrations.

## License

This workspace is a local tutorial project. Add your chosen license if you plan to publish.

If you want, I can also:
- Add example appsettings.json (safeguarded template)
- Add Bootstrap Icons CDN snippet to _Layout.cshtml
- Create an EF Core migration template

## Routes

The application uses conventional MVC routing (default route pattern: `{controller=Home}/{action=Index}/{id?}`). Key routes available in this project:

- Home
  - GET  /                    -> HomeController.Index (Home page)
  - GET  /Home/Privacy        -> HomeController.Privacy (Privacy policy)

- Students (Student management)
  - GET  /Students/List       -> StudentsController.List (list all students)
  - GET  /Students/Add        -> StudentsController.Add (show add form)
  - POST /Students/Add        -> StudentsController.Add (create new student) — requires antiforgery token
  - GET  /Students/Details/{id} -> StudentsController.Details (view student details)
  - GET  /Students/Edit/{id}  -> StudentsController.Edit (show edit form)
  - POST /Students/Edit       -> StudentsController.Edit (submit edits) — requires antiforgery token
  - POST /Students/Delete     -> StudentsController.Delete (delete student) — uses POST form with antiforgery token

Notes:
- All POST actions expect antiforgery tokens. Ensure forms include `@Html.AntiForgeryToken()` or use the `form` tag helper, which injects it automatically.
- Route URLs shown above follow the default routing configuration. If you changed routing in Startup/Program, adjust accordingly.

