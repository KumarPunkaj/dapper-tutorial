---
PermaID: 1000169
Name: Parameter Anonymous
---

# Dapper - Parameter Anonymous 

## Description
Dapper make it simple & safe (SQL Injection) to use parameter by supporting anonymous type.

### Single
Execute a single time a SQL Command.

```csharp
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
	var affectedRows = connection.Execute(sql, new {CustomerName = "Mark"});

	Console.WriteLine(affectedRows);
	
	// Only for see the Insert.
	var customer = connection.Query<Customer>("Select * FROM CUSTOMERS WHERE CustomerName = 'Mark'").ToList();

	FiddleHelper.WriteTable(customer);
}
```
{% include component-try-it.html href='https://dotnetfiddle.net/Z1iRIQ' %}  

### Many
Execute many times a SQL Command

```csharp
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{			
	var affectedRows = connection.Execute(sql,
	new[]
	{
	new {CustomerName = "John"},
	new {CustomerName = "Andy"},
	new {CustomerName = "Allan"}
	}
	
	Console.WriteLine(affectedRows);
)
```
{% include component-try-it.html href='https://dotnetfiddle.net/fvRKsY' %}  
