# Components | Dynamic Components
<br>


### Use the `DynamicComponent` built-in component to dynamically render a component specified by type.

// TODO: complement description

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

