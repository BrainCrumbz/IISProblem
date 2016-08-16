# IISProblem
ASP.NET Core solution showing problem with IISExpress and renamed project directory

## Steps to recreate solution (and problem)

1. Open VS 2015 Community Edition
2. Create new project and select *ASP.NET Core Web Application (.NET Core)* project type
3. Name solution as e.g. `BrainCrumbz.IISProblem`, name project as e.g. `BrainCrumbz.IISProblem.MyProject`
5. Select *Empty* web application type
6. Save all. Do not run, nor build, so not to create hidden `.vs\config\applicationhost.config` yet
7. Remove project
8. Rename **project** folder to e.g. just `MyProject`
9. Add back existing project from renamed folder
10. Add explicit project name, title and version in `project.json`:

  ```json
  "name": "BrainCrumbz.IISProblem.MyProject",
  "title": "BrainCrumbz.IISProblem.MyProject",
  "version": "0.0.0",
```
1. Make sure *IIS Express* profile is selected (the default)
2. Run

## Expected

* VS stays running in debug mode. Browser shows *Hello world* text
* Windows Event Viewer, Applications log, shows a warning by *IIS Express*. We're seeing that on working web applications as well, it seems related to Bitdefender ([issue 309](https://github.com/aspnet/Tooling/issues/309) and [StackOverflow](http://stackoverflow.com/questions/34033654/asp-net-5-web-app-not-running-in-debug-mode-in-iis-express)) and it seems not having effects on this issue

> The directory specified for caching compressed content C:\Users\@@@USERNAME@@@\AppData\Local\Temp\iisexpress\IIS Temporary Compressed Files\Clr4IntegratedAppPool is invalid.  Static compression is being disabled

* Following warning, there's an Information event by *IIS Express AspNetCore Module* with success message:

> Process '10016' started successfully and is listening on port '11928'.

## Actual

* VS stops and leaves debug mode unexpectedly. Browser shows *Server unreachable* page
* Windows Event Viewer, Applications log, shows same warning as before
* Following warning, there's an Error event by *IIS Express AspNetCore Module*:

> Failed to start process with commandline '"C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Web Tools\ProjectSystem\VSIISExeLauncher.exe" -debug -p "C:\Program Files\dotnet\dotnet.exe" -a "D:\WS\NET\ASP.NET-Core\BrainCrumbz.IISProblem\src\MyProject\bin\Debug\netcoreapp1.0\MyProject.dll" -pidFile "C:\Users\@@@USERNAME@@@\AppData\Local\Temp\tmpF450.tmp" -wd "D:\WS\NET\ASP.NET-Core\BrainCrumbz.IISProblem\src\MyProject"', ErrorCode = '0x80004005'.

## Environment

* Windows development machine
* Visual Studio 2015 Community Edition Version 14.0.25424.00 Update 3
* Microsoft .NET Core Tools (Preview 2) 14.1.20810.0
  * `dotnet --version` reports *1.0.0-preview2-003121*
  * Also installed brand new one, *DotNetCore.1.0.0-VS2015Tools.Preview2.0.1.exe*, with no improvement
