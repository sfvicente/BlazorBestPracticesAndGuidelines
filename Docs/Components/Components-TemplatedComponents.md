# Components | Templated Components
<br>


## `RenderFragment`

The `RenderFragment` is a delegate that generates segments of UI content to a `RenderTreeBuilder`.
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


## Template Context Parameters
<br>


### Set the `Context` attribute on the a `RenderFragment` child element to change the implicit parameter name.

To change the implicit parameter named `context` for a `RenderFragment` component argument, use the `Context` attribute to specify the desired parameter. In 
the example below, instead of using `context.Id`, the `Context` attribute is assigned `user` that allows us to use `user.Id`:

```csharp
<TableTemplate Items="users">
    <TableHeader>
        <th>ID</th>
        <th>Username</th>
        <th>Email</th>
    </TableHeader>
    <RowTemplate Context="user">
        <td>@user.Id</td>
        <td>@user.Username</td>
        <td>@user.Email</td>
    </RowTemplate>
</TableTemplate>
```

@code {
    ...
}
<br>