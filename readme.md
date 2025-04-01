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