# HTTP Communication | Headers
<br>


### Use the `Referer` request header to make application decisions based on the page the user came from.

To customize the application (such as providing custom content for a user) based on the page from where the user came from, you can use the `Referer` request header. The `Referer` header contains the address of the previous web page from which a link to the currently requested page was followed.
Here is how you can access the header in your application:

1. Register the `HttpContextAccessor` service in your `Startup.cs` file:

```csharp
public void ConfigureServices(IServiceCollection services)
{
	services.AddHttpContextAccessor();
}
```

2. Include the `HttpContext` in your component using dependency injection:

```csharp
@inject Microsoft.AspNetCore.Http.IHttpContextAccessor httpContextAccessor
```

3. Retrieve the value of the `Referer` request header:

```csharp
protected override void OnInitialized()
{
    var referer = httpContextAccessor.HttpContext.Request.Headers["Referer"];
}
```
<br>

