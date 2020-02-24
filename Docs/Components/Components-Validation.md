# Components | Validation
<br>


### To determine if changes have been made to an `EditForm` use the `IsModified()` methods of the `EditContext` class.

The `EditContext` class provide the following methods to determine if an `EditForm` has been changed or not:

```csharp
/// <summary>
/// Determines whether any of the fields in this <see cref="EditContext"/> have been modified.
/// </summary>
/// <returns>True if any of the fields in this <see cref="EditContext"/> have been modified; otherwise false.</returns>
public bool IsModified()
{
	// If necessary, we could consider caching the overall "is modified" state and only recomputing
	// when there's a call to NotifyFieldModified/NotifyFieldUnmodified
	foreach (var state in _fieldStates)
	{
		if (state.Value.IsModified)
		{
			return true;
		}
	}

    return false;
}

/// <summary>
/// Determines whether the specified fields in this <see cref="EditContext"/> has been modified.
/// </summary>
/// <returns>True if the field has been modified; otherwise false.</returns>
public bool IsModified(in FieldIdentifier fieldIdentifier)
	=> _fieldStates.TryGetValue(fieldIdentifier, out var state)
		? state.IsModified
		: false;

/// <summary>
/// Determines whether the specified fields in this <see cref="EditContext"/> has been modified.
/// </summary>
/// <param name="accessor">Identifies the field whose current validation messages should be returned.</param>
/// <returns>True if the field has been modified; otherwise false.</returns>
public bool IsModified(Expression<Func<object>> accessor)
	=> IsModified(FieldIdentifier.Create(accessor));
```
<br><br>


### Use the `ObjectGraphDataAnnotationsValidator` component instead of  `DataAnnotationsValidator` to validate collections or complex types.

 The `DataAnnotationsValidator` component only validates top-level properties of a model. It does not validate collections or complex-type properties of model class.

Blazor provides the `ObjectGraphDataAnnotationsValidator` component to validate entire object models including collections and complex-type properties.

To use the `ObjectGraphDataAnnotationsValidator` component, install the `Microsoft.AspNetCore.Blazor.DataAnnotations.Validation` package from _NuGet_.

```html
<EditForm Model="@model" OnValidSubmit="HandleValidSubmit">
	<ObjectGraphDataAnnotationsValidator />
	...
</EditForm>
```

All complex and collection type model properties must be decorated with `ValidateComplexType` attribute.

```csharp
using System.ComponentModel.DataAnnotations;

public class Customer
{
	[Required]  
	public string Name { get; set; }  

	[Required]  
	[ValidateComplexType]  
	public Address BillingAddress { get; set; }  
  
	public Customer()
	{  
		this.BillingAddress = new BillingAddress();  
	}
}
```

Note: `ObjectGraphDataAnnotationsValidator` was introduced in ASP<span>.<span>NET Core updates in .NET Core 3.1 Preview 2 as experimental support for object graph validation using data annotations.
<br>
