# Application Development | Debugging
<br>


### To debug Blazor WebAssembly applications, use browser development tools or Visual Studio IDEs.

_Blazor WebAssembly_ applications can be debugged using the following tools:
- Browser development tools in Edge (version 80 or later) and Chrome (version 70 or later)
- Visual Studio Integrated development environments (IDEs)
<br><br><br>


### To Log or print comments during code execution, use `Console.Write` and `Console.WriteLine`.

Similar to `console.log` in JavaScript, Blazor applications can use `Console.Write` and `Console.WriteLine` to log or print comments during execution.

```csharp
Console.WriteLine("This is content logged to output window");
```

<br>


### To view more detailed information on exceptions that occur within your application, enable `DetailedErrors`.

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


### To enable detailed information on exceptions that occur within your application for development only, enable `DetailedErrors` based on the `IWebHostEnvironment` property `IsDevelopment`.

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


### Add a delay at the start of the `OnInitialized` or `OnInitialized¿sync` methods if breakpoints are not being hit.

Due to the time required for the _Blazor_ framework's debugging proxy to execute, breakpoints set in the `OnInitialized`{Async} `OnInitializedAsync` methods might not trigger.

Adding a delay at the start of the method code will allow the debug proxy enough time to launch before the breakpoints is hit.

```csharp
protected override void OnInitialized()
{
	Thread.Sleep(10000);
    ...
}
```

```csharp
protected override void OnInitializedAsync()
{
	await Task.Delay(10000);
    ...
}
```


