# Dapper Plus - Bulk Update

## Description
UPDATE entities using Bulk Operation.

- [Update single](#example---update-single)
- [Update many](#example---update-many)
- [Update with relation (One to One)](#example---update-with-relation-one-to-one)
- [Update with relation (One to Many)](#example---update-with-relation-one-to-many)

## Example - Update Single
UPDATE a single entity with Bulk Operation.

```csharp
DapperPlusManager.Entity<Customer>().Table("Customers"); 

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
    connection.BulkUpdate(customers);
}	
```
{% include component-try-it.html href='https://dotnetfiddle.net/nl29KW' %}

## Example - Update Many
UPDATE many entities with Bulk Operation.

```csharp
DapperPlusManager.Entity<Customer>().Table("Customers");

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
    connection.BulkUpdate(customers);
}	
```
{% include component-try-it.html href='https://dotnetfiddle.net/Z2ttwQ' %}

## Example - Update with relation (One to One)
UPDATE entities with a one to one relation with Bulk Operation.

```csharp
DapperPlusManager.Entity<Supplier>().Table("Suppliers").Identity(x => x.SupplierID);
DapperPlusManager.Entity<Product>().Table("Products").Identity(x => x.ProductID);

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{	
    connection.BulkUpdate(suppliers).ThenForEach(x => x.Product.SupplierID = x.SupplierID).ThenBulkUpdate(x => x.Product);
}		
```
{% include component-try-it.html href='https://dotnetfiddle.net/ueWXDF' %}

## Example - Update with relation (One to Many)
UPDATE entities with a one to many relation with Bulk Operation.

```csharp
DapperPlusManager.Entity<Supplier>().Table("Suppliers").Identity(x => x.SupplierID);
DapperPlusManager.Entity<Product>().Table("Products").Identity(x => x.ProductID);

using (var connection = new SqlCeConnection("Data Source=SqlCe_W3Schools.sdf"))
{
    connection.BulkUpdate(suppliers).ThenForEach(x => x.Products.ForEach(y => y.SupplierID =  x.SupplierID)).ThenBulkUpdate(x => x.Products);
}
```
{% include component-try-it.html href='https://dotnetfiddle.net/2coF4V' %}
