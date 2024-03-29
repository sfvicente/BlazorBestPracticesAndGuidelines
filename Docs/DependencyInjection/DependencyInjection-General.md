# Dependency Injection | General
<br>


## Service Registration
<br>


### To register services for dependency injection use, add the service to the application's service collection.

Configuration for the application service collection can be done in the `Main` entry method for the application:

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var builder = WebAssemblyHostBuilder.CreateDefault(args);
        ...
        builder.Services.AddTransient<ICartService, CartService>();
        ...

        await builder.Build().RunAsync();
    }
}
```
<br>


## Requesting Services
<br>


### To inject a service in a component, use the `@inject` directive.

The `@inject` directive allows adding services from the service container to components via dependency injection.

Dependencies are injected in components after the component instance is created and before the `OnInitialized` or `OnInitializedAsync` lifecycle events
are triggered. Due to this behavior, dependencies cannot be used in the constructor of the component. However, those will be available in the
`OnInitialized` and `OnInitializedAsync` methods.

To consume services, declare the `@inject` dependency in the component using the dependency name: 

```csharp
@page "/checkout"
@using Services
@inject ICartService CartService

...

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


### Use the `[Inject]` attribute to inject services into component classes.

The `[Inject]` indicates that the associated property should have a value injected from the service provider during the class initialization.

Using the `[Inject]` attribute, you can add a service to a class-only component. In the example below, the `CartService` service is injected into the component through property injection.

```csharp

	...
    public class CartComponent : ComponentBase  
    {  
        [Inject]  
        protected ICartService cartService { get; set; }  
    }  
}  
```
<br>


### Use constructor injection to add required services to a service.

Unlike components, when developing services, the `@inject` directive and the `[Inject]` attribute is not supported. To allow for dependencies to be injected, constructor injection
is used.

```csharp
public class HttpCrawler
{
	public HttpCrawler(HttpClient httpClient)
	{
		...
	}
}
```
<br>


### Always define the necessary dependencies of services explicitly in their constructors.

By explicitly defining the dependencies in the constructors, services can not be instantiated or used without it.

todo: complement description

```csharp

// todo: add example
```
<br>


### Consider assigning injected dependencies to read-only fields or properties.

A `readonly` modifier prevents the assignment to the field after the constructor exits. This action protects the assignment of other references
to the object inside the class.

todo: complement description

```csharp
public class CartService : ICartService
{
    private readonly IProductService productService;

    public CartService(IProductService productService)
    {
		...

        this.productService = productService;
    }
}
```
<br>


## Service Design
<br>


### Avoid static classes and members when designing services for dependency injection.

Static classes are classes which cannot be instantiated.

todo: add description

```csharp

// todo: add example
```
<br>


### Avoid direct instantiation of dependent classes within services when designing services for dependency injection.

When performing direct instantiation of dependent classes within services, it couples the implementation of those classes to a specific implementation.

todo: complement description

```csharp

// todo: add example
```
<br>



## `IDisposable`

The `IDisposable` interface provides a mechanism for releasing unmanaged resources.
<br>


### Don't register `IDisposable` instances with a transient lifetime.

Use the factory pattern instead.

todo: complement description

```csharp

// todo: add example
```
<br>


### Don't call `Dispose` on a dependency within the class that has received that `IDisposable` dependency.

todo: complement description

```csharp

// todo: add example
```
<br>


## Service Lifetime
<br>


### Use scopes to control the lifetimes of services.

<Scopes aren't hierarchical, and there's no special connection among scopes.>

todo: complement description

```csharp

// todo: add example
```
<br>


## Service Container
<br>


### Always use the built-in container unless an unsupported feature is required.

.NET supports dependency injection and provides `IServiceProvider` as the built-in service container. `IServiceProvider` does not
currently support the following features:

- Property injection
- Injection based on name
- Child containers
- Custom lifetime management
- `Func<T>` support for lazy initialization
- Convention-based registration

Unless one or more of these features is required, always use the built-in container.

<br>

