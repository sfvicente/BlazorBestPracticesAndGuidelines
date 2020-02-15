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

