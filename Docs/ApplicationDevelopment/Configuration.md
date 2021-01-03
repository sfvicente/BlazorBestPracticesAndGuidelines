# Application Development | Configuration
<br>


### Use the `UseStartup()` method to control `Startup` class activation.

The `UseStartup()` method has an overload that allows you to provide a factory method for controlling `Startup` class activation. This is useful if you want to pass 
additional parameters to `Startup` that are initialized along with the host.

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var logger = CreateLogger();
        var host = Host.CreateDefaultBuilder()
            .ConfigureWebHost(builder =>
            {
                builder.UseStartup(context => new Startup(logger));
            })
            .Build();

        await host.RunAsync();
    }
}
```

Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/
<br>


### To disable pre-rendering in _Blazor Server_ applications, change the application component render mode to `Server`.

To disable prerendering for a _Blazor Server_ application, edit the Pages/_Host.cshtml file. Modify the render-mode attribute value of the Component Tag Helper to `Server`.

```csharp
<component type="typeof(App)" render-mode="Server" />
```

Applies To: Blazor Server
Additional Tags: Application, Render Mode
<br>