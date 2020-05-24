# Security | Authorization
<br>


### Use the `Authorize` attribute to control authorization to a _Razor_ component.

```cshtml
@page "/"
@attribute [Authorize]

<p>This is only visible if user is signed in.<p>
```
<br>


### Use the `Roles` parameter of the `[Authorize]` attribute to perform role-based authorization.

```cshtml
@page "/"
@attribute [Authorize(Roles = "admin, owner")]

<p>This is only visible for signed-in administrators and owners.<p>
```
<br>


### Use the `Policy` parameter of the `[Authorize]` attribute to perform policy-based authorization.

```cshtml
@page "/"
@attribute [Authorize(Policy = "allow-printing")]

<p>This is only visible if users satisfies the 'allow-printing' policy.</p>
```
<br>


