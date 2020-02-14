# Components | Lifecycle
<br>

**Do not call `StateHasChanged()` inside a components `Dispose()` method.**

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

