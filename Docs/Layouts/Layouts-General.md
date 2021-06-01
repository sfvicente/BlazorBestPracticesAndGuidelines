# Layouts | General
<br>


## `@layout` Directive
The `@layout` directive specifies a layout for routable Razor components that define `@page` directives.
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

<br><br><br>


### Do not add `@layout` directives to the root __Imports.razor_ file.

Adding a `@layout` directive to the __Imports.razor_ file results in an infinite loop of layouts in the application.

<br><br><br>


### To set the default application layout, specify the layout in the `Router` component.

You can configure the default application layout in the `DefaultLayout` attribute of the `RoutView` element. This element is located
inside the `Router` component.

<sub>App.razor</sub>
```csharp
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MyLayout)" />
    </Found>
    <NotFound>
        <p>Sorry, there's nothing at this address.</p>
    </NotFound>
</Router>
```

Setting a default layout is a recommended practice due to the ability to override layouts per component and per folder.

<br><br><br>
