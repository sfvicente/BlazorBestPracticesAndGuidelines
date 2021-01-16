# Components | Communication
<br>


## `@ref` attribute

The `@ref` attribute provide a way to reference a component instance to allow sending commands to that instance.
<br/>


### Use `@ref` attribute to capture references to child components

In order to capture the reference to a child component, add the `@ref` attribute to the declaration of the child component in the markup section. You also need to define a field with the same type as the child component.

```
<AddTaskDialogBox @ref="addTaskDialogBox" ... />

@code {
	private AddTaskDialogBox addTaskDialogBox;
	...
}
```
<br/>


### Use component references to issue commands to a component instance.

After a reference field is populated with the child component instance, you can invoke methods on the component instance.

```
<AddTaskDialogBox @ref="addTaskDialogBox" ... />

@code {
	private AddTaskDialogBox addTaskDialogBox;

	private void OnAddTaskButtonClick()
	{
		addTaskDialogBox.Show();
	}
	...
}
```
<br/>


### Do not use component references to mutate the state of child components.

`ToDo: Example`

Instead, use normal declarative parameters to pass data to child components. Use of normal declarative parameters result in child components that re-render at the correct times automatically.

`ToDo: Example`
<br/>


### Use the `OnAfterRenderAsync` or `OnAfterRender` methods to manipulate components via references after the component has finished rendering.

Variables that hold references to components via `@ref` attribute are only populated after the component is rendered and its output includes the component element.

```
<AddTaskDialogBox @ref="addTaskDialogBox" ... />

@code {
	ToDo: code sample
}
```
<br/>


### Use a lambda expression or assign the event handler delegate in the `OnAfterRenderAsync` or `OnAfterRender` methods to use a reference variable with an event handler.

Using a lambda expression or assigning the event handler delegate in the `OnAfterRenderAsync` or `OnAfterRender` methods ensures that the reference variable is assigned
before the event handler is assigned.

```

	ToDo: code sample
```

<br/>




