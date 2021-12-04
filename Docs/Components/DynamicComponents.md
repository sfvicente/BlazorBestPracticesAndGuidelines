# Components | Dynamic Components
<br>

## General
<br>


### Use the `DynamicComponent` built-in component to dynamically render a component specified by type.

The `DynamicComponent` is a component that renders another component dynamically according to its `Type` parameter. It allows an application
to present components without the need to add programming logic or check for specific types.

```cs
<DynamicComponent Type="@myComponentType" />
```

// TODO: complement code samples

<br>


## Parameters
<br>


### To pass parameters to a dynamically-renderer component, use the `Parameters` attribute.

Data can be passed to dynamic components through the `Parameters` attribute using a dictionary. A `IDictionary<string, object>` can be used
where the `string` is the name of the parameter, and the `object` is the parameter's value.

```cs
<DynamicComponent Type="@myComponentType" Parameters="@myParameters" />

@code {
    IDictionary<string, object> myParameters = new Dictionary<string, object>();

    ...
}
```

// TODO: complement code samples

<br>


### Avoid the use of catch-all parameters when using dynamically-renderer components.

// TODO: Complement content

The use of catch-all parameters with `DynamicComponent` should be avoided. 

// TODO: complement code samples

<br>