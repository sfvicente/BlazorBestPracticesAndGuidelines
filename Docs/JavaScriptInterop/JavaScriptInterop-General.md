# JavaScript Interop | General

JavasScript interopability is the ability to invoke invoke JavaScript functions from .NET methods and .NET methods from JavaScript functions by _Blazor_ applications.
<br>


## `IJSRuntime` Interface

The `IJSRuntime` interface represents an instance of a JavaScript runtime to which calls may be dispatched.
<br>


### Inject the `IJSRuntime` interface into a component to issue _JavaScript_ interop calls within the component.

Inject the `IJSRuntime` abstraction into the _Razor_ component using the `inject` keyword.

```csharp
 @page "/"
 @inject IJSRuntime JSRuntime

 <h1 id="title">Hello, world!</h1>
```
<br>


### To execute _JavaScript_ interop calls from within a class, inject the `IJSRuntime` abstraction into the class.

Inject the `IJSRuntime` abstraction into a class via constructor injection.

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


### Inject the `IJSRuntime` abstraction with the `[Inject]` attribute for dynamic content generation with `BuildRenderTree`.

Inject the `IJSRuntime` abstraction using property injection.

```
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

ToDo: Add description

```
ToDo: Example
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

In most scenarios modifying the DOM with Javascript isn't recommended because JavaScript can interfere with Blazor's change tracking.

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