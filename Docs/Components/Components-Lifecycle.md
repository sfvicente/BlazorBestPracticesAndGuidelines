# Components | Lifecycle

The _Blazor_ framework includes a system to control order of eents in the lifetime of components. The each component has synchronous and asynchronous lifecycle methods which 
can be overriden to extend and configure component initialization and rendering.
<br><br>

## General
<br>

### Do not access parameters from within a constructor of a component class.

Accessing parameters should not be done inside a constructor. The properties will be null within the execution of the constructor of an instance. Use the `OnInitialized()` 
or `OnInitializedAsync()` methods instead.

The following code example won't work as the property `InlineClass` won't be set to any value:

```csharp
public abstract class MyCustomComponent: ComponentBase
{
	[Parameter]
	public string InlineClass { get; set; }
	
	public InlineClassMapper Mapper { get; }

	protected MyCustomComponent()
	{
		this.Mapper = new InlineClassMapper(this.InlineClass);
	}
}
```

At the time that the constructor is executed, the parameter has not yet been set. It will be available when `OnInitialized` or `OnInitializedAsync` is called.

```csharp
public abstract class MyCustomComponent: ComponentBase
{
	[Parameter]
	public string InlineClass { get; set; }

	public InlineClassMapper Mapper { get; }
	...

	protected override void OnInitialized()
	{
		this.Mapper = new InlineClassMapper(this.InlineClass);
	}
}
```

Additional Tags: Parameters
<br><br>


## `StateHasChanged()` Method
<br>

### Do not call `StateHasChanged()` inside a components `Dispose()` method.

Calling `StateHasChanged()` inside the `Dispose()` method of a component is not supported. The `StateHasChanged()` method might be invoked as part of
tearing down the renderer, so requesting UI updates at that point is not possible.

The following code should not be used:

```csharp
@using System
@implements IDisposable
...

@code { 
	public void Dispose()
	{
		...
		StateHasChanged();
	}
}
```

Additional Tags: `Dispose()`
<br><br>


## Component Disposal
Component disposal is a mechanism for releasing resources, such as memory that was allocated or locks that have been acquired.
<br><br>


### Implement `IDisposable` to dispose of resources when the component is removed from the UI

Components can implement `IDisposable` to dispose of resources when the component is removed from the UI. `IDispose` can be implemented by using the `@implements` directive:

```csharp
@using System
@implements IDisposable

...

@code {
	...

	public void Dispose()
	{
		... 
	}
}
```

Additional Tags: Unmanaged Resources
<br><br>


### Always implement `IDisposable` in a component to unsubscribe to events.

Not unregistering event handlers is a common cause of memory leaks. To avoid that, any event handlers previously set should be removed during the disposal of the component.

When an even event handler is attached and not removed after the component or the handler is disposed, even if it is not being referenced, it leads to the object instance
containing the handler to remain in memory longer than necessary. Also, if the component is rendered again, it normally runs the same logic to attach another event handler 
instance to the same event. This will lead to issue if the component is disposed and created frequently.

```csharp
@using System
@implements IDisposable

...

@code {
    [Parameter]
    public Cart cart { get; set; }

    protected override async Task OnInitializedAsync()
    {
        await base.OnInitializedAsync();
        cart.OnCartChanged += CartChanged;
    }

    public void Dispose()
    {
        cart.OnCartChanged -= CartChanged;
    }
}
```

Additional Tags: Event, Event Handling, Memory Leak
<br><br>


### Use `IAsyncDisposable` for the asynchronous release of allocated resources.

The `IAsyncDisposable` interface provides a mechanism for releasing unmanaged resources asynchronously.

todo: complement description

todo: add code

Additional Tags: Asynchronous
<br><br>


### Always use `DisposeAsync` instead of `Dispose()` for asynchronous disposal tasks.

todo: complement description

```csharp
public async ValueTask DisposeAsync()
{
    ...
}
```

<br><br>