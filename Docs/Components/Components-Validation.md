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