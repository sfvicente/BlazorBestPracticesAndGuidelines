# Application Development | Debugging
<br>

**To view more detailed information on exceptions that occur within your application, enable `DetailedErrors`**

Add the code below to your _Startup.cs_ to see more details about exceptions happening in your application:

```csharp
public class Startup
{
	public void ConfigureServices(IServiceCollection services)
	{
		...
		services.AddRazorPages();
		services.AddServerSideBlazor()
		    .AddCircuitOptions(opt =>
		    {
				opt.DetailedErrors = true;
			});
		...
	}
}
```
<br><br>


**To enable detailed information on exceptions that occur within your application for development only, enable `DetailedErrors` based on the `IWebHostEnvironment` property `IsDevelopment` **

Add the code below to your _Startup.cs_ to see more details about exceptions happening in your application in development only:

```csharp
public class Startup
{
	private readonly IWebHostEnvironment environment;

	public Startup(IConfiguration configuration, IWebHostEnvironment env)
	{
		Configuration = configuration;
		this.environment = env;
	}

	public void ConfigureServices(IServiceCollection services)
	{
		...
		services.AddRazorPages();
		services.AddServerSideBlazor()
		    .AddCircuitOptions(opt =>
		    {
				opt.DetailedErrors = this.environment.IsDevelopment();
			});
		...
	}
}
```
<br><br>
