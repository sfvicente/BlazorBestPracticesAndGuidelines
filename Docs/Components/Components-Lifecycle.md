# Components | Lifecycle
<br>


### Do not access parameters from within a constructor of a component class. Use the `OnInitialized()` or `OnInitializedAsync()` methods instead.

The following code example won't work as the property `InlineClass` won't be set to any value. The property will be null within the execution of the constructor of an instance.

```csharp
public abstract class MyCustomComponent: ComponentBase
{
	[Parameter]
	public string InlineClass { get; set; }
	
	protected MyCustomComponent()
	{
		this.Mapper = new InlineClassMapper(this.InlineClass);
	}
}
```

At the time that the constructor is executed, the parameter is not yet set. It will be available when `OnInitialized` or `OnInitializedAsync` is called.

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
<br><br>


### Do not call `StateHasChanged()` inside a components `Dispose()` method.

Calling `StateHasChanged()` inside a components `Dispose()` method ins't supported. `StateHasChanged` might be invoked as part of tearing down the renderer, so requesting UI updates at that point isn't supported.

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
<br><br>


### Implement `IDisposable` to dispose of resources when the component is removed from the UI

Blazor components can implement `IDisposable` to dispose of resources when the component is removed from the UI. A Razor component can implement `IDispose` by using the `@implements` directive:

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
<br>


