# Application Development | Environment
<br>

### To determine the application's environment, use the 'Environment' property of the 'IWebAssemblyHostEnvironment' interface.

The `IWebAssemblyHostEnvironment` provides information about the hosting environment where an application is being executed. It is possible to determine the current environment in
a component by injecting `IWebAssemblyHostEnvironment` and reading its `Environment` property:

```csharp
@page "/"
@using Microsoft.AspNetCore.Components.WebAssembly.Hosting
@inject IWebAssemblyHostEnvironment HostEnvironment

<p>Environment: @HostEnvironment.Environment</p>
```

<br>