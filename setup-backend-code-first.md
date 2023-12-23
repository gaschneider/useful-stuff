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

## Adding Classes/Tables

Now that we have the EF installed, we need to start creating our classes that will become tables in the DB.
Create a new project that will serve as our Data project(you can create as a Class Library project), then create a folder that will contain your Entities, you can call it Entities or Models or another name that fits you better(I will be using Models for the sake of reference in this step-by-step)
Now inside our Models folder, lets create our first class.

In this tutorial I will be using as example part of my classes from my To Do List app.
So, right click in Models, Add, then New Item, `ToDoList.cs` will be our first class.
In this class, lets declare:
- Id: type int
- Name: type string - Default value: "My list"
- Description: type string - Default value: "To Do list"

## Adding a context

Now we need to create the class that will manage our DB tables vs our classes, we call it our DB Context.
Right click on the Data project level, Add, then New Item, `ToDoListsContext.cs` will be our context.

Now inside this class we need to first declare it inheritance from DbContext, this way we will be telling to the EntityFramework
that this class will be used to identify our entities/tables.

Lets also declare a constructor in here, like below:
```
public ToDoListsContext(DbContextOptions<ToDoListsContext> options) : base(options)
{ }
```

We need to declare our previous created class (ToDoList) as a property in the following way:
`public DbSet<ToDoList> ToDoLists { get; set; }`
