# Components | Dynamic Components
<br>


### Use the `DynamicComponent` built-in component to dynamically render a component specified by type.

The `DynamicComponent` is a component that renders another component dynamically according to its `Type` parameter. It allows an application
to present components without the need to add programming logic or check for specific types.

```cs
<DynamicComponent Type="@myComponentType" />
```

Data can be passed to dynamic components through the `Parameters` attribute using a dictionary:

```cs
<DynamicComponent Type="@myComponentType" Parameters="@myParameters" />

@code {
    IDictionary<string, object> myParameters = new Dictionary<string, object>();

    ...
}
```

// TODO: complement code samples

<br>

