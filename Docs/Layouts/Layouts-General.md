# Layouts | General
<br>

### To explicitly specify a layout for an individual component, use the `@layout` directive.

The most explicit level of specifying a layout template is in the component itself by using the `@layout` directive.

In the example below, the content of the component is inserted into the `AdminLayout` at the location where the `@Body` instruction has been set.

```csharp
@layout AdminLayout
@page "/admin/"

<h2>Administration Area</h2>
...

code {
	...
}
```

If you specify the layout in a component, it overrides the default layout set in the router or any `@layout` directive that has been imported from __Imports.razor_.

<br>


### Do not add `@layout` directives to the root __Imports.razor_ file.

Adding a `@layout` directive to the __Imports.razor_ file results in an infinite loop of layouts in the application.

To set the default application layout, specify the layout in the `Router` component.

TODO: add code

<br>
