# Components | Templated Components
<br>


### To reuse rendering logic without declaring actual components, define a `RenderFragment` that emits UI.

It's possible to emit UI without creating components. In a component's `@code` block, define a `RenderFragment` delegate to render content
in the component's render area.

```csharp
<h1>Hello, world!</h1>

@RenderTitle

@code {
    RenderFragment RenderTitle = __builder =>
    {
        <div>
            <p>This is a title!</p>
       </div>
    };
}
```

<br>