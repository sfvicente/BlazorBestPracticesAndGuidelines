# Security | Authorization
<br>


### Use the `Authorize` attribute to control authorization to a _Razor_ component.

```cshtml
@page "/"
@attribute [Authorize]

<p>This is only visible if user is signed in.<p>
```
<br>