# Dependency Injection | General
<br>


## `@inject` directive

The `@inject` directive allows adding services from the service container to components via dependency injection.


### To inject a service in a component, use the `@inject` directive.

TODO: Description

```csharp
TODO: Example
```
<br>


### Use multiple `@inject` statements to inject additional services in a component.

If you require more services in a component, add the required services via additional `@inject` statements.

```csharp
@page "/checkout"
@using Services
@inject ICartService CartService
@inject ICustomerService CustomerService

@if (_products != null)
{
	...
}

@code { 
	private IReadOnlyList<Products> _products;

	protected override async Task OnInitializedAsync()
	{
		_products = await CartService.GetAllProductsAsync();
		...
	}
}
```
<br>


### Do not use the `@inject` directive on derived components for services already injected in the base class.

Assuming you have the following base component class:

```csharp
TODO: Add code
```

If a component inherits from that base class, the @inject directive is not required on the component. The service injected in the base class is automatically made available on
derived components.

```csharp
TODO: Add code
```
<br>

