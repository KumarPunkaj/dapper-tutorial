---
layout: default
title: Dapper - Transaction
permalink: transaction
---

{% include template-h1.html %}

## Description
Dapper support the transaction and TransactionScope

## Transaction

Begin a new transaction from the connection and pass it in the transaction optional parameter.

{% include template-example.html %} {% highlight csharp %}
string sql = "INSERT INTO Customers (CustomerName) Values (@CustomerName);";

using (var connection = new SqlConnection(FiddleHelper.GetConnectionStringSqlServerW3Schools()))
{
	connection.Open();
	
	using (var transaction = connection.BeginTransaction())
	{
		var affectedRows = connection.Execute(sql, new {CustomerName = "Mark"}, transaction: transaction);
		
		transaction.Commit();
		
		Console.WriteLine(affectedRows);
	}
}
{% endhighlight %}
{% include component-try-it.html href='https://dotnetfiddle.net/RlZRFz' %}

## TransactionScope

Begin a new transaction scope before starting the connection

{% include template-example.html %} {% highlight csharp %}
// using System.Transactions;

using (var transaction = new TransactionScope())
{
	var sql = "Invoice_Insert";

	using (var connection = My.ConnectionFactory())
	{
		connection.Open();

		var affectedRows = connection.Execute(sql,
			new {Kind = InvoiceKind.WebInvoice, Code = "Single_Insert_1"},
			commandType: CommandType.StoredProcedure);
	}

	transaction.Complete();
}
{% endhighlight %}
