# JavaScript Interop | JavaScript Isolation

 JavaScript isolation allows you to confine the scope of imported JavaScript to specific components or areas of your
 application, preventing conflicts or unintended interactions with other scripts or global variables.
<br>


### Use JavaScript isolation to avoid polluting the global namespace with imported JavaScript.

Always leverage JavaScript isolation in when incorporating external scripts or custom JavaScript functionalities. This
practice promotes modularity, reduces the potential for naming collisions, and enhances the overall maintainability of 
your Blazor application.

todo: add examples

<br>


### Use JavaScript isolation to avoid forcing consumers of a library or components to import its JavaScript dependencies.

todo: add description
todo: add examples

<br>


### To render UI generated from JavaScript libraries within a component, add an empty element with a reference and update it in the `OnAfterRenderAsync` first render.

todo: add description

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
