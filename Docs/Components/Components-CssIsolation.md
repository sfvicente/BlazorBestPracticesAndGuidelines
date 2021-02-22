# Components | CSS Isolation

CSS isolation is a mechanism that allows styles to be defined and used for specific component and optionally it's child components. It prevents dependencies on global styles
and helps to avoid styling conflicts among components and libraries.
<br>


### Use the `::deep` combinator in CSS to cascade styles down to child components.

Although CSS isolation only applies to the current component by default, styles can be configured to be applied to child components. To cascade styles to child 
components without the need to create component-specific CSS file, use the `::deep` combinator in the associated CSS.

// TODO: complement description

// TODO: complement code samples

`Pages/Parent.razor.css`:

```css
::deep h1 {
    color: blue;
    font-family: Tahoma, Arial, Verdana, sans-serif;
}
```
<br>


### To disable automatic bundling, add the `DisableScopedCssBundling` _MSBuild_ property to the project file.

The scoped file publish and loading runtime mechanism for CSS isolation can be disabled by configuring the build process. It is achieve by adding the `DisableScopedCssBundling`
_MSBuild_ property to the project file. This will allow for custom build processes.

```html
<PropertyGroup>
  <DisableScopedCssBundling>true</DisableScopedCssBundling>
</PropertyGroup>
```

By disabling scoped Css bundling, the following actions will be required for CSS isolation to work:
1. Retrieving the scoped CSS files from the `obj` directory
2. Publish the scoped CSS files
3. Load the scoped CSS files during runtime

// TODO: complement description
<br>