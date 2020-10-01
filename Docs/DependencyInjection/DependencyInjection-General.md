# Dependency Injection | General
<br>


## `@inject` directive

The `@inject` directive allows adding services from the service container to components via dependency injection.


### To inject a service in a component, use the `@inject` directive.

TODO: Description
TODO: Example

<br>


### Use multiple `@inject` statements to inject additional services in a component.

If you require more services in a component, add the required services via additional `@inject` statements.

``` csharp
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