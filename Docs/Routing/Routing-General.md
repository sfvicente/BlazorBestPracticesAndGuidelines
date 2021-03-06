# Routing | General
<br>


## Route Templates

Route templates are mechanisms to match URLs to components. You can define route templates for components by adding the `@page` directive to the top of the component definition.
<br>


### To allow multiple URLs to resolve to a component, add additional route templates using the `page` directive.

It is possible to add multiple route templates to a component. In the example below, both `/admin` and `/administration` will resolve to the same component which will then
process the requests.

```csharp
@page "/admin"
@page "/administration"

<h1>User Administration</h1>
```
<br>


### To create optional route parameters add additional  `@page` declarations in a component.

Although there is no specific mechanism for optional route parameters, the functionality can be achieve by using multiple `@page` declarations.

```csharp
@page "/counter"
@page "/counter/{CounterId:int}"

<h1>Counter</h1>
<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
```
<br>


### To capture paths across multiple folder boundaries in components, use catch-all route parameters.

A catch-all route parameter allows a component to capture multiple paths even

Catch-all parameters need to be added at the end of the URL of the route template with a `string` type. The route value will be copied to the defined parameter in the component.

```csharp
@page "/catch-all/{*pageRoute}"

@code {
    [Parameter]
    public string PageRoute { get; set; }
}
```

todo: include route examples.

Applies To: .NET 5
<br>


## `NavigationManager`

The `NavigationManager` provides an abstraction for querying and managing URI navigation in Blazor applications.
<br>


### Use the `Uri` property of the `NavigationManager` class to obtain the current absolute URI.

The `NavigationManager` class provides an abstraction for querying and managing URI navigation. In order to retrieve the current URL, inject the `NavigationManager`
class into the _Razor_ component. It is located inside the `Microsoft.AspNetCore.Components` assembly. Then use the `Uri` property to determine the current absolute URI:

```csharp
@page "/"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>

Current Url: @NavigationManager.Uri
```

This returns a string with the full URL, including hostname.
<br>


### To obtain the current relative URL or fragments of the current URL, convert the `NavigationManager.Uri` into a Uri type.

todo: complement description

```csharp
@page "/"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>

@(new Uri(navigationManager.Uri).PathAndQuery)
```

<br>

### Use the `NavigateTo` method of the `NavigationManager` class to navigate to a specific URI.

The `NavigationManager` class provides an abstraction for querying and managing URI navigation. Use the `NavigateTo` to navigate to the desired component.

```csharp
@page "/navigate"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>
<button class="btn btn-primary" @onclick="NavigateToCheckout">Checkout</button>

@code {
	private void NavigateToCheckout()
	{
		NavigationManager.NavigateTo("checkout");
	}
}
```
<br>


### Use the `LocationChanged` event to determine when the URL in the browser is changed.

`LocationChanged` is an event that is triggered whenever the URL in the browser is modified. It passes an instance of `LocationChangedEventArgs` which provides the the URL :

```csharp
// TODO: Example

```
<br>


### Use the `forceLoad` parameter of the `NavigateTo` method to instruct Blazor to bypass its own routing system and perform an HTTP request to the server to retrieve the content to display.

Using `forceLoad` will make the browser navigate to the new URL through a server request.

```csharp
@page "/navigate"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>
<button class="btn btn-primary" @onclick="NavigateToTerms">Terms & Conditions</button>

@code {
	private void NavigateToTerms()
	{
		NavigationManager.NavigateTo("https://mydomain.com/terms.html");
	}
}
```
<br>


### Do not use `forceLoad` to navigate to an off-site URI.

Using `forceLoad` is not required in order to navigate to an off-site URI. Calling `NavigateTo` to another domain will perform a full browser navigation.

```csharp
@page "/navigate"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>
<button class="btn btn-primary" @onclick="NavigateToBlazerHomepage">Blazor Homepage</button>

@code {
	private void NavigateToBlazorHomepage()
	{
		NavigationManager.NavigateTo("https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor");
	}
}
```
<br>


### To navigate to a new browser tab, use _JavaScript Interop_ with the `IJSRuntime` object.

Use _blank as the value for the third parameter, which will notify the system that the url needs to be opened in the new browser tab.

TODO: complement description.

```csharp
@inject IJSRuntime jsRuntime

<button @onclick="HandleNavigateToNewTab">Navigate to New Tab</button>

@code {

    public async Task HandleNavigateToNewTab()
    {
        string url = "/counter";

        await jsRuntime.InvokeAsync<object>("open", url, "_blank");
    }
}
```

Additional Tags: Javascript Interop
<br>


### Use the `IsNavigationIntercepted` property of the `NavigationManager` to determine whether navigation was initiated through code or HTML.

The `IsNavigationIntercepted` indicates whether the navigation was initiated via code or via an HTML navigation. If the `IsNavigationIntercepted` is set to `false`, the navigation was initiated by using the `NavigationManager.NavigateTo()` method in the code. If the value of the property is set to `true`, then _Blazor_ has intercepted the navigation instead of allowing the browser to navigate to the new URL, which would result in a request to the server. Any request not initiated using the `NavigateTo()` method will be intercepted.

```csharp
@implement IDisposable
@inject NavigationManager NavigationManager

protected override void OnInitialized()
{
	NavigationManager.LocationChanged += LocationChanged;
	base.OnInitialized();
}

void LocationChanged(object sender, LocationChangedEventArgs e)
{
	string method = e.IsNavigationIntercepted ? "HTML" : "code";
	
	Debug.WriteLine($"Navigation to '{e.Location}' initiated via  '{navigationMethod}'");
}

void IDisposable.Dispose()
{
	NavigationManager.LocationChanged -= LocationChanged;
}
```
<br>


## 404 Error
The 404 error is an action that happens when a user tries to reach a non-existent page on a site. It can be generated due to the user clicking a broken link, attempting
to access a page that has been deleted, or a mistyped a URL.
<br>

### Provide a 404 page when the application fails to match a URL to a component.

404 is a standard response code that is returned by a server to indicate that a page was successfully requested but the application was unable to locate it.

```csharp
<Router AppAssembly="typeof(Program).Assembly">
	<Found Context="routeData">
		<RouteView RouteData="routeData" />
	</Found>
	<NotFound>
		<div class="content">
			<h1># Page not found</h1>
			<p>We're sorry, we couldn't find the page you requested. Return to the <a href="/">home page.</a>
			</p>
		</div>
	</NotFound>
</Router>
```

TODO: Image
<br>


### Don't use `RedirectToPage` to perform a redirect to a component.

Do not use the `PageBase.RedirectToPage()` method to perform redirection to a component in a _Blazor_ based applications. `RedirectToPage()` is used to perform HTTP redirects to
_Razor_ pages. Instead, inject the `NavigationManager` component and use it's `NavigateTo()` method.

```csharp
@inject NavigationManager NavigationManager

// TODO: Complement example

NavigationManager.NavigateTo("counter/2");

```
<br>


## Other
<br>


### To obtain all the routes of an application programmatically, use reflection.

To obtain the list of all routes contained in an application, iterate through all component types using reflection and select those that have a `RouteAttribute`:

```csharp
var components = assembly
    .ExportedTypes
    .Where(t => t.IsSubclassOf(typeof(ComponentBase)));

var routes = components
    .Select(component => GetRouteFromComponent(component))
    .Where(config => config is not null)
    .ToList();

...

private string GetRouteFromComponent(Type component)
{
    var attributes = component.GetCustomAttributes(inherit: true);
    var routeAttribute = attributes.OfType<RouteAttribute>().FirstOrDefault();

    if (routeAttribute is null)
    {
        return null;
    }

    return routeAttribute.Template;
}
```

<br>