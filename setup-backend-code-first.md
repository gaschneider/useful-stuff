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

Right click on your project level, then select `Manage nuget Packages`, for this project we gonna need to install the following packages:
- EntityFrameworkCore
- EntityFrameworkCore.Relational
- EntityFrameworkCore.SqlServer

In the next step we will be creating a new project for classes, and in this new project we gonna need to install the following packages:
- EntityFrameworkCore
- EntityFrameworkCore.SqlServer
- EntityFrameworkCore.Tools

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

## Setting the connectionString

Now we need to set the connection string to our SQL DB, since we will be using local, we need to go to appsettings.json
lets create a section like below:
```
"ConnectionStrings": {
  "ToDoListDB": "Server=(LocalDb)\\MSSQLLocalDB;Database=ToDoLists;Trusted_Connection=True;"
},
```

This will reference our code to the DB it will create.

## Updating Startup.cs

In our Startup.cs file, we need to update it to use that connection string, to do this we will change the method `ConfigureServices` to look like below:
```
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();
    services.AddDbContext<ToDoListsContext>(option => option.UseSqlServer(Configuration.GetConnectionString("ToDoListDB")));
}
```

This means it will add the db context using our DbContext class and our connection string.

## Adding migration

Now, we need to add a migration(this will convert our classes into SQL scripts that will create/update our tables).
To do this, open Package Manager Console, you can do this through `View` -> `Other windows` -> `Package Manager Console`
In here, we need to set Default Project to our Data project, also we need to right click in our main project and set it as Startup Project

As next step we need to type in: `Add-Migration "Initial_Migration"`
This command will generate our first migration

## Creating our DB

And here having a migration we can finally run in the Package Manager Console the following command:
`Update-Database`
This command will take care of comparing our local DB with our migrations and update it to the latest.

Now we should be able to go to our SSMS and see our DB and tables in there as follow:

![image](https://github.com/gaschneider/useful-stuff/assets/16023844/4ee16cae-76b5-40c7-964f-dc08a7f8791a)


For the full code check my other repo [ToDo-List](https://github.com/gaschneider/ToDo-List)
