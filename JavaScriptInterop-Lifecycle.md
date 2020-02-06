# Javascript Interop | Lifecycle
<br>

**Use the `OnAfterRenderAsync` component method to execute JavaScript code after your components have been rendered.**

If there is Javascript code that needs to execute after a component has been rendered, you should use the OnAfterRenderAsync method.

```
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

