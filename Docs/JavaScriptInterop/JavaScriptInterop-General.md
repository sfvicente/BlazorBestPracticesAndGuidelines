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


### Inject the `IJSRuntime` abstraction into a class to execute JSInterop calls from within the class.

Inject the `IJSRuntime` abstraction into a class via constructor injection.

```
TODO: Example
```
<br>


### Inject the `IJSRuntime` abstraction with the `[Inject]` attribute for dynamic content generation with `BuildRenderTree`.

Inject the `IJSRuntime` abstraction using property injection.

```
[Inject]
IJSRuntime JSRuntime { get; set; }
```
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