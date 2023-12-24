# C# Errors
### Here I will list a couple errors that can be misleading.

1. When using EntityFrameworkCore for code first and calling Add-Migration:
<br>You should call EntityFrameworkCore\Add-Migration instead, without the EntityFrameworkCore\ in front you are actually refering to EntityFramework and it will raise error on it.
