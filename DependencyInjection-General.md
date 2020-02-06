# Dependency Injection | General
<br>

**Use multiple `@inject` statements to inject different services in a component.**

If you require more services in a component, add the required services via additional `@inject` statements.

```  
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
<br><br>
