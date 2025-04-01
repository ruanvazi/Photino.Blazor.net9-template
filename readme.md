# Photino.Blazor Desktop App Template (.NET 9)

A simple, step-by-step guide to setting up a desktop application using **Photino.Blazor** and **Blazor** with **.NET 9**.

---

## 📌 Prerequisites

Ensure you have installed:

- [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- [Visual Studio Code](https://code.visualstudio.com/) or [Visual Studio](https://visualstudio.microsoft.com/)

---

## 🚀 Getting Started

Follow these simple steps to set up your **Photino.Blazor** desktop application:

### Step 1: Initialize a Blazor Project

Create a new Blazor Web project:

```bash
dotnet new blazor
```

### Step 2: Install Photino.Blazor Package

Add the **Photino.Blazor** NuGet package:

```bash
dotnet add package Photino.Blazor
```

---

## ⚙️ Project Configuration

### Step 3: Add Minimal `index.html`

Create the following file:

```
wwwroot/index.html
```

Include this minimal HTML content:

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
    <app>Loading...</app>
    <script src="_framework/blazor.webview.js"></script>
</body>
</html>
```

### Step 4: Update `App.razor`

Remove the following script reference from your `App.razor` file (if present):

```html
<script src="_framework/blazor.web.js"></script>
```

### Step 5: Modify `.csproj` File

Replace your project file (`.csproj`) contents with the following:

```xml
<Project Sdk="Microsoft.NET.Sdk.razor">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net9.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

  <ItemGroup>
    <Content Update="wwwroot\**">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </Content>
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Photino.Blazor" Version="4.0.13" />
  </ItemGroup>

</Project>
```

---

## 🛠️ Application Setup

### Step 6: Update `Program.cs`

Replace the contents of `Program.cs` with the following:

```csharp
using Microsoft.Extensions.DependencyInjection;

namespace Photino.Blazor.net9_template
{
    class Program
    {
        [STAThread]
        static void Main(string[] args)
        {
            var appBuilder = PhotinoBlazorAppBuilder.CreateDefault(args);

            appBuilder.Services.AddLogging();

            // Register root component and selector
            appBuilder.RootComponents.Add<App>("app");

            var app = appBuilder.Build();

            // Customize window title
            app.MainWindow.SetTitle("Photino Blazor Sample");

            AppDomain.CurrentDomain.UnhandledException += (sender, error) =>
            {
                app.MainWindow.ShowMessage("Fatal Exception", error.ExceptionObject.ToString());
            };

            app.Run();
        }
    }
}
```

---

## 🧹 Cleanup & Adjustments

### Step 7: Remove `@rendermode` from Pages

- Remove the `@rendermode InteractiveServer` directive from `Counter.razor`.
- Remove the `@attribute [StreamRendering]` directive from `Weather.razor`.

### Step 8: Project Type Adjustment and Cleanup

- Modify the project SDK in `.csproj` to use Razor SDK:

```xml
<Project Sdk="Microsoft.NET.Sdk.razor">
```

- Ensure `Program.cs` uses:

```csharp
using Microsoft.Extensions.DependencyInjection;
```

- Delete unnecessary files:

  - `./Components/Pages/Error.razor`
  - Remove `<ImportMap />` directive from `./Components/App.razor`

---

## 🎉 Launch your Application!

Build and run your project using the following command:

```bash
dotnet run
```

Enjoy building your Photino.Blazor Desktop App!

---

## 📖 Resources & Documentation

- [Photino.Blazor GitHub Repository](https://github.com/tryphotino/photino.Blazor)
- [.NET Blazor Official Documentation](https://learn.microsoft.com/en-us/aspnet/core/blazor)
- [.NET 9.0 Official Site](https://dotnet.microsoft.com/)

---

Happy coding! 🚀✨