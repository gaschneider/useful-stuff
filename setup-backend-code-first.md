# How to setup a .NET Core WebApp with Entity Framework Code First and SSMS

Here I will describe step by step how to setup a fully functional WebApp:
- in .NET Core 
- using Entity Framework Code First 
- Microsoft SQL Server 

to allow integration with frontend through REST API

PS: I will be using Visual Studio 2022 Community in this tutorial.

## New Project

Start by creating a new project of type ASP .NET Core Web API, in this step you gonna need to:
- Give a name to your project
- Give a name to your solution
- Select the framework(for this tutorial, we will use .NET 8.0)
- You can choose if it will have some authentication, but for a simple one, we will go with none.

With all that done, we can start by creating it.

## Installing necessary packages

In this step we gonna start installing the necessary packages to make our Entity Framework Code First available.

Right click on your project level, then select `Manage nuget Packages`, in the screen opened, go to the `Browse` tab and search for `EntityFrameork`.
Once the package is located, select it, then on the right side a button for installing will be available.
Click on it and wait for the installation to be completed.


