# Security | Authorization
<br>


## `AuthorizeView` Component

The `AuthorizeView` component displays content depending on the user's authorization status.


### Use the `AuthorizeView` component to selectively display UI depending on whether the user is authorized to view it.

The component simplifies the process to display information for an authorized user. It is suitable choice if there is no need to access authorization data from code.

```cshtml
<AuthorizeView>
    This is only displayed to authenticated users.
</AuthorizeView>
```
<br>


### Use the `context` variable exposed by `AuthorizeView` to access information about the signed-in user.

The `AuthorizeView` component exposes a `context` variable of type `AuthenticationState`. The `AuthenticationState` class provides information about the currently authenticated user.

```cshtml
<AuthorizeView>
    <h1>Signed-in Username: @context.User.Identity.Name</h1>
</AuthorizeView>
```
<br>


### Use the `AuthorizeView` component to display information about the logged-in user but not use it in procedural logic.

If there is no need to access authorization data from code but you need to display it, you can use the `<AuthorizeView>`. The component exposes a context variable of type
AuthenticationState, which can be used to display information about the current user:

```cshtml
<AuthorizeView>
    <h1>Hello, @context.User.Identity.Name!</h1>
    This is only displayed to authenticated users.
</AuthorizeView>
```
<br>


### Use the `<Authorizing>` tag to display content while authentication occurs when performing asynchronous authentication.

The `AuthorizeView` component allows the display of content while authentication occurs. Consider the scenario where your _Blazor WebAssemly_ application needs to
call an external authentication service. By default, no content is showed while the authentication is being performed. You can use the `Authorizing` tag to display UI
content during the operation.

```csharp
<AuthorizeView>
    <Authorized>
        <h1>Username: @context.User.Identity.Name!</h1>
        <p>You are currently authenticated.</p>
    </Authorized>
    <Authorizing>
        <h1>Authentication in progress</h1>
        <p>Please wait while we perform authentication...</p>
    </Authorizing>
</AuthorizeView>
```

Applies to: Blazor WebAssembly
<br>


## `[Authorize]` Attribute

The `[Authorize]` attribute specifies that the class or method it is applied to, requires the defined authorization.


### Use the `[Authorize]` attribute to control authorization to a _Razor_ component.

```cshtml
@page "/"
@attribute [Authorize]

<p>This is only visible if user is signed in.<p>
```
<br>


### Use the `Roles` property of the `[Authorize]` attribute to perform role-based authorization.

The `AuthorizeAttribute.Roles` property gets or sets a comma delimited list of roles that are allowed to access the resource.

```cshtml
@page "/"
@attribute [Authorize(Roles = "admin, owner")]

<p>This is only visible for signed-in administrators and owners.<p>
```
<br>


### Use the `Policy` property of the `[Authorize]` attribute to perform policy-based authorization.

The `AuthorizeAttribute.Policy` property gets or sets the policy name that determines access to the resource.

```cshtml
@page "/"
@attribute [Authorize(Policy = "allow-printing")]

<p>This is only visible if users satisfies the 'allow-printing' policy.</p>
```
<br>