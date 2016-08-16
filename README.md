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

## Actual

* VS stops and leaves debug mode unexpectedly. Browser shows *Server unreachable* page

## Environment

* Visual Studio 2015 Community Edition Version 14.0.25424.00 Update 3
* Microsoft .NET Core Tools (Preview 2) 14.1.20810.0
  * `dotnet --version` reports *1.0.0-preview2-003121*
  * Also installed brand new one, *DotNetCore.1.0.0-VS2015Tools.Preview2.0.1.exe*, with no improvement
