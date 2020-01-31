### Components | Communication

**Use `@ref` attribute to capture references to child components**

In order to capture the reference to a child component, add the `@ref` attribute to the declaration of the child component in the markup section. You also need to define a field with the same type as the child component.

```
<AddTaskDialogBox @ref="addTaskDialogBox" ... />

@code {
	private AddTaskDialogBox addTaskDialogBox;
	...
}
```
<br/><br/>





**Do not use component references to mutate the state of child components**

`ToDo: Example`

Instead, use normal declarative parameters to pass data to child components. Use of normal declarative parameters result in child components that re-render at the correct times automatically.

`ToDo: Example`
<br><br>





