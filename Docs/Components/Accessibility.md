# Components | Accessibility
<br>


### Use the `FocusOnNavigate` component to set the UI focus to an element based on a CSS selector after navigating from one page to another.

Upon using the Router to navigate to a new page, the `FocusOnNavigate` component can be used to set the focus to a specific CSS element of that page. The
element is then idenfied by screen readers. The objective is to ensure that navigating between pages in single-page apps is properly reported to users
of screen readers.

TODO: complement description

```cs
<Router AppAssembly="@typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
        <FocusOnNavigate RouteData="@routeData" Selector="h1" />
    </Found>
    <NotFound>
        ...
    </NotFound>
</Router>
```

TODO: complement description

<br>