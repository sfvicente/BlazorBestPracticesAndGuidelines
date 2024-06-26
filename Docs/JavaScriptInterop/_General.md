# JavaScript Interop | General

JavasScript interopability is the ability to invoke invoke JavaScript functions from .NET methods and .NET methods from JavaScript functions by _Blazor_ applications.
<br>


## `IJSRuntime` Interface

The `IJSRuntime` interface represents an instance of a JavaScript runtime to which calls may be dispatched.
<br>


### To perform _JavaScript_ interop calls within a _Razor_ component, inject the `IJSRuntime` interface into the component.

Inject the `IJSRuntime` abstraction into the _Razor_ component using the `inject` keyword.

```csharp
 @page "/"
 @inject IJSRuntime JSRuntime

 <h1 id="title">Hello, world!</h1>
```
<br>


### To execute _JavaScript_ interop calls from within a class, inject the `IJSRuntime` abstraction into the class.

The `IJSRuntime` abstraction allows dispatching calls to the JavaScript runtime. It can be injected into a class via constructor injection:

```csharp
public class JsInteropExtensions
{
    private readonly IJSRuntime jsRuntime;

    public JsInteropClasses(IJSRuntime jsRuntime)
    {
        this.jsRuntime = jsRuntime;
    }

    public ValueTask<string> CartUpdated(string data)
    {
        return jsRuntime.InvokeAsync<string>("handleCartChanged", cartUpdate.items, cartUpdate.action);
    }
}
```
<br>


### To perform dynamic content generation with `BuildRenderTree`, inject the `IJSRuntime` abstraction using the `[Inject]` attribute.

Inject the `IJSRuntime` abstraction using property injection.

```csharp
[Inject]
IJSRuntime JSRuntime { get; set; }
```
<br>


### Consider performing synchronous calls from _.NET_ to _JavaScript_ to improve performance.

Performing synchronous interop calls have decreased overhead and can result in fewer render cycles as there is no need for `await` actions on results.

To allow the application to make calls to _Javascript_ in a synchronous way, the `IJSRUntime` needs to be cast to `IJSInProcessRuntime`. The interface `IJSInProcessRuntime` represents
an instance of a _JavaScript_ runtime to which calls may be dispatched.

```csharp
@inject IJSRuntime JSRuntime

...
@code {
    protected override void OnInitialized()
    {
        CartService.OnCartUpdated += cartUpdate =>
        {
                var jsInProcess = (IJSInProcessRuntime)JSRuntime;
                var value = jsInProcess.Invoke<string>("cartContentUpdated");
                ...
        };
    }
}
```

Synchronous calls can only be perform from _Blazor WebAssembly_ applications as _JavaScript_ interop calls on _Blazor Server_ applications are sent over a network connection.

Applies to: Blazor WebAssembly
Additional Tags: Performance
<br>


### Wrap JavaScript interop calls within `try-catch` statements.

Wrapping JavaScript interop calls within `try-catch` statements in Blazor components is a recommended practice to enhance
error handling and application stability. By handling potential exceptions proactively, you can prevent unexpected crashes
and provide a smoother user experience, especially when integrating with external JavaScript libraries or APIs. Additionally,
logging or displaying meaningful error messages within the catch block helps with debugging and troubleshooting issues related
to JavaScript interop.

```csharp
@page "/interop-example"
@using Microsoft.JSInterop

<h3>Interop Example</h3>

<button @onclick="CallJsInterop">Call JavaScript Interop</button>

@code {
    [Inject]
    protected IJSRuntime JSRuntime { get; set; }

    private async Task CallJsInterop()
    {
        try
        {
            // Attempt to invoke a JavaScript function via interop
            await JSRuntime.InvokeVoidAsync("exampleJsInteropFunction");
            Console.WriteLine("JavaScript interop call succeeded.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"JavaScript interop call failed: {ex.Message}");
            // Handle the exception appropriately (e.g., log, notify user, etc.)
        }
    }
}
```
<br>


### Place custom JavaScript code at the bottom of the __Host.cshtml_ file, just below the script section that includes the Blazor code.

```
<script src="_framework/blazor.server.js"></script>
<script>
        window.MyMethods =
        {
            myMethod1: function (element) {
                window.alert(element.id);
            }
        };
</script>
```
<br>


### Avoid modifying the Document Object Model (DOM) directly with _JavaScript_.

In most scenarios, modifying the DOM with Javascript isn't recommended because JavaScript can interfere with Blazor's change tracking.

Consider the example below:

```csharp
@using Microsoft.JSInterop
@inject IJSRuntime JSRuntime

<div @ref="divElement">Text during render</div>

@code {
    private ElementReference divElement;

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await JSRuntime.InvokeVoidAsync(
                "setElementText", divElement, "Text after render");
        }
    }
}
```
<br>


## `JSRuntimeExtensions`

The `JSRuntimeExtensions` class provides a set of extensions for the `IJSRuntime`.


### To call a _JavaScript_ function that doesn't return a value, use the `InvokeVoidAsync` method of the `JSRuntimeExtensions` class.

The `InvokeVoidAsync` can be used to call a _JavaScript_ function asynchronously, when the function does not return a value.

```csharp
@inject IJSRuntime JSRuntime

TODO: Complement code

@code {
    private ElementReference username;

    public async Task X()
    {
        await JSRuntime.InvokeVoidAsync(
            "jsFunctions.X", X);
    }
}
```
<br>


### Always use `ValueTask<TResult>` when performing interop with generic types and returning a value.

TODO: add description

```csharp
public static ValueTask<T> GenericMethod<T>(this ElementReference elementRef, 
    IJSRuntime jsRuntime)
{
    TODO: complement code

    return jsRuntime.InvokeAsync<T>(
        "x.x", elementRef);
}
```
<br>


## Application Details
<br>


### To obtain the current IP address of the application, use a 3rd party API.

Currently, the _Blazor Framework_ does not have a mechanism to retrieve the current IP address for the application. However, it is possible to use a service
such as _Ipify_ that will return the address in various formats. Use either JS Interop or an HTTP client to retrieve the required information.

TODO: Complement description

```csharp

var httpClient = new HttpClient();
var ip = await httpClient.GetStringAsync("https://api.ipify.org");

TODO: complement code

```

Additional Tags: IP Address, HttpClient
<br>


## Configuration
<br>


### To change the default timeout for all interop calls, set the `JSInteropDefaultCallTimeout` property in `Startup.ConfigureServices`.

TODO: improve description
<JS interop may fail due to networking errors and should be treated as unreliable. By default, a Blazor Server app times out JS interop calls on the server after one minute.
If an app can tolerate a more aggressive timeout,> set the timeout using the `JSInteropDefaultCallTimeout` property in `Startup.ConfigureServices`.

The following code sets the default timeout for interop calls as 10 seconds.

```csharp
services.AddServerSideBlazor(
    options => options.JSInteropDefaultCallTimeout = TimeSpan.FromSeconds(10));
```
<br>


### To change the default timeout for a interop call, set the `cancellationToken` parameter of `InvokeAsync` method.

TODO: improve description
<JS interop may fail due to networking errors and should be treated as unreliable. By default, a Blazor Server app times out JS interop calls on the server after one minute.
If an app can tolerate a more aggressive timeout,> set the timeout for a function using the `cancellationToken` parameter of `InvokeAsync`.

The following code sets the default timeout for an interop call as 10 seconds.

```csharp
var result = await JSRuntime.InvokeAsync<string>("myFunction", 
    TimeSpan.FromSeconds(10), new[] { "Arg1" });
```
<br>


## Performance/Optimization
<br>


### Consider sending the content of interop calls with large payloads in smaller chunks and processing the messages as a `Stream`.

TODO: improve description
<In Blazor WebAssembly, the framework doesn't impose limits on the size of inputs and outputs of JS interop calls.>
<In Blazor Server, the result of a JS interop call is limited by the maximum payload size enforced by SignalR, which defaults to 32 KB>

<Increasing the SignalR limit comes at the cost of requiring the use of more server resources, and it exposes the server to increased risks from a malicious user. Additionally,
reading a large amount of content in to memory as strings or byte arrays can also result in allocations that work poorly with the garbage collector, resulting in additional
performance penalties.>

TODO: Add description

TODO: Add sample code

Applies To: Blazor Server
Additional Tags: Configuration, SignalR
<br>


