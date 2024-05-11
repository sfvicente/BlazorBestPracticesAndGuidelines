# JavaScript Interop | JavaScript Isolation

 JavaScript isolation allows you to confine the scope of imported JavaScript to specific components or areas of your
 application, preventing conflicts or unintended interactions with other scripts or global variables.
<br><br>


### Use JavaScript isolation to avoid polluting the global namespace with imported JavaScript.

Always leverage JavaScript isolation in when incorporating external scripts or custom JavaScript functionalities. This
practice promotes modularity, reduces the potential for naming collisions, and enhances the overall maintainability of 
your Blazor application.

```razor
@page "/example"
@using Microsoft.JSInterop

<h3>Example Component</h3>

@code {
    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            // Load script.js in isolation
            await JSRuntime.InvokeVoidAsync("import", "./js/script.js");
        }
    }

    private async Task CallScriptFunction()
    {
        // Call showAlert function from script.js
        await JSRuntime.InvokeVoidAsync("showAlert");
    }
}
```

<br>


### Use JavaScript isolation to avoid forcing consumers of a library or components to import its JavaScript dependencies.

JavaScript isolation in Blazor components or libraries, allows developers to abstract away complex JavaScript dependencies,
improving the usability and maintainability of their code. Consumers benefit from a cleaner, more encapsulated API without
the need to handle external script imports, ultimately enhancing the overall developer experience and component reusability.

```razor
// MyReusableComponent.razor

<h3>My Reusable Component</h3>

@code {
    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            // Load JavaScript dependency in isolation
            await JSRuntime.InvokeVoidAsync("import", "./js/myReusableComponent.js");
        }
    }

    public async Task CallJavaScriptMethod()
    {
        // Call a JavaScript function from isolated dependency
        await JSRuntime.InvokeVoidAsync("myReusableComponent.doSomething");
    }
}
```
<br>


### To render UI generated from JavaScript libraries within a component, add an empty element with a reference and update it in the `OnAfterRenderAsync` first render.

By adding empty elements with references and updating them in the `OnAfterRenderAsync` method's first render, you ensure
that JavaScript-generated UI components are properly integrated into Blazor's component lifecycle. This approach helps
maintain a clean separation between Blazor's rendering system and JavaScript-based UI functionalities, ensuring a robust
and predictable user interface.

```razor
@page "/map-example"
@using Microsoft.JSInterop

<h3>Map Example</h3>
<div id="mapContainer"></div>

@code {
    protected override async Task OnAfterRenderAsync(bool firstRender)
    {
        if (firstRender)
        {
            // Initialize and render the map after first render
            await JSRuntime.InvokeVoidAsync("initializeMap", "mapContainer");
        }
    }
}
```

<br>
