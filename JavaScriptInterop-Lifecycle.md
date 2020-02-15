# Javascript Interop | Lifecycle
<br>

**Use the `OnAfterRenderAsync` component method to execute JavaScript code after the app is fully rendered and the client connection is established.**

If there is Javascript code that needs to execute after a component has been rendered, you can use the `OnAfterRenderAsync` component lifecycle event to delay JavaScript interop calls until after the connection with the browser is established.

```csharp
 @page "/"
 @inject IJSRuntime jsRuntime

 <h1 id="myid" @ref=MyElementReference>Hello, world!</h1>
 
@code{
    ElementReference MyElementReference;

    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            await JSRuntime.InvokeAsync<object>("MyJSMethods.myMethod", MyElementReference);
        }

    }
}

```
<br/><br/>


**When using `OnAfterRender()` or `OnAfterRenderAsync()`, use the `firstRender` parameter to ensure that initialization work is only performed once.**

The `OnAfterRender()` and `OnAfterRenderAsync()` lifecycle methods are useful for performing tasks such as _JavaScript_ interop or interacting with values received from `@ref`. 

```csharp
protected override Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        TODO: Example
    }
    return Task.CompletedTask;
}
```
When the `firstRender` variable is true, which occurs only when the component is rendered for the first time, you should initialize your _JavaScript_ objects.
<br/><br/>


