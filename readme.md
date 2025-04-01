# Template Photino.Blazor dotnet9.0 Desktop App

## Step one - Init Project

```bash
dotnet new blazor
```

## Step Two - Install Photino.Blazor

```bash
dotnet add package Photino.Blazor
```

## Step Three - Add Minimal index.html

Add the file

```bash
wwwroot/index.html
```

Insert the contents

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

## Step Four - Update App.razor

Remove the following from App.razor

```html
    <script src="_framework/blazor.web.js"></script>
```

## Step Five - Update Project csproj file

```txt
<Project Sdk="Microsoft.NET.Sdk.Web">

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

## Step Six - Update Program.cs

```csharp
namespace Photino.Blazor.net9_template
{
    class Program
    {
        [STAThread]
        static void Main(string[] args)
        {
            var appBuilder = PhotinoBlazorAppBuilder.CreateDefault(args);

            appBuilder.Services
                .AddLogging();

            // register root component and selector
            appBuilder.RootComponents.Add<App>("app");

            var app = appBuilder.Build();

            // customize window
            app.MainWindow
                .SetTitle("Photino Blazor Sample");

            AppDomain.CurrentDomain.UnhandledException += (sender, error) =>
            {
                app.MainWindow.ShowMessage("Fatal exception", error.ExceptionObject.ToString());
            };

            app.Run();

        }
    }
}
```

## Step Seven - Remove @rendermode From Pages

Remove @rendermode InteractiveServer from Counter.razor

@attribute [StreamRendering] from Weather.razor

## Step Eight - Change Project Type to Razor

Modify csproj to target "Microsoft.NET.Sdk.razor"

```text
<Project Sdk="Microsoft.NET.Sdk.razor">
```

Modify Program.cs to use "Microsoft.Extensions.DependencyInjection"

```csharp
using Microsoft.Extensions.DependencyInjection;
```

Delete ./Components/Pages/Error.razor

Delete ```<ImportMap />``` from ./Components/App.razor
