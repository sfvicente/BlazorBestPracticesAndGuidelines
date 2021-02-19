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