# Components | Forms & Validation
<br>


## `EditForm` Component

The `EditForm` class renders a form element that cascades an EditContext to descendants.
<br>


### Always instantiate the `Model` before assigning it to an `EditForm`.

TODO: add description

```csharp
private UserModel userModel = new UserModel();
```
<br>


### Do not use both a `Model` and an `EditContext` for the same `EditForm` to perform validation.

In order for the EditForm to perform validation, it requires either a `Model` or an `EditContext` to be assign to it. It is not possible to assignment both. Doing so will generates
a runtime error.

TODO: add description

```csharp

	/// TODO: add code sample
```
<br>


### Use `OnSubmit` event of the `EditForm` to use custom code to trigger validation and verification of field data.

The `EditForm` component has an `OnSubmit` that can be used to perform additional tasks when the form submission is triggered. In the example below, the `HandleSubmit` method is
invoked when the submit button is pressed.

```csharp
<EditForm EditContext="@editContext" OnSubmit="@HandleSubmit">

	...
	<button type="submit">Submit</button>
</EditForm>

@code {
	...
	
	private async Task HandleSubmit()
	{
		/// Validate and verify field data.
		...
	}
```
<br>


### Use the `IsModified()` methods of the `EditContext` class to determine if changes have been made to an `EditForm`.

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


### Specify custom validation class names when integrating with CSS frameworks, like Bootstrap.

To specify custom validation class names, create a class derived from FieldCssClassProvider and set it on the EditContext instance.

```csharp
var editContext = new EditContext(model);
editContext.SetFieldCssClassProvider(new MyFieldClassProvider());

// ...

class MyFieldClassProvider : FieldCssClassProvider
{
    public override string GetFieldCssClass(EditContext editContext, in FieldIdentifier fieldIdentifier)
    {
        var isValid = !editContext.GetValidationMessages(fieldIdentifier).Any();
        
        return isValid ? "legit" : "totally-bogus";
    }
}
```

Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/


## `ValidationSummary`

The `ValidationSummary` class displays a list of validation messages from a cascaded `EditContext`.
<br>


### To prevent displaying `ValidationSummary` component messages before triggering form submission, use the _CSS_ `display` property with the 'OnValidSubmit' event handling.

The example below make the `ValidationSummary` component visible only when the submit button is pressed. The visibility of the component is controlled via the `display` _CSS_ property.

```csharp
<EditForm EditContext="@editContext" OnValidSubmit="@HandleOnValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary style="@validationSummaryStyle" />

    ...

    <button type="submit" disabled="@formInvalid">Submit</button>
</EditForm>

@code {
    private string validationSummaryStyle = "display:none";

    ...

    private void HandleOnValidSubmit()
    {
        validationSummaryStyle = "display:block";
    }
}
```
<br>