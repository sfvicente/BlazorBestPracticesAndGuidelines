# Routing

**Use the `Uri` property of the `NavigationManager` class to obtain the current absolute URI**

The `NavigationManager` class provides an abstraction for querying and managing URI navigation. Use the `Uri` to determine the current absolute URI.

```
@page "/"
@inject NavigationManager NavigationManager

<h1>Hello, world!</h1>

Current Url: @NavigationManager.Uri
```
<br/><br/>

**Use the `NavigateTo` method of the `NavigationManager` class to navigate to a specific URI**

The `NavigationManager` class provides an abstraction for querying and managing URI navigation. Use the `NavigateTo` to navigate to the desired component.

```
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
<br/><br/>

**Use the `LocationChanged` event to determine when the URL in the browser is changed.**

`LocationChanged` is an event that is triggered whenever the URL in the browser is modified. It passes an instance of `LocationChangedEventArgs` which provides the the URL :

```
Example
```
<br/><br/>


**Use the `forceLoad` parameter of the `NavigateTo` method to instruct Blazor to bypass its own routing system and perform an HTTP request to the server to retrieve the content to display**

Using `forceLoad` will make the browser navigate to the new URL through a server request.

```
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
<br/><br/>


**Do not use `forceLoad` to navigate to an off-site URI.**

Using `forceLoad` is not required in order to navigate to an off-site URI. Calling `NavigateTo` to another domain will perform a full browser navigation.

```
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
<br/><br/>


**Use the `IsNavigationIntercepted` property of the `NavigationManager` to determine whether navigation was initiated through code or HTML**

The `IsNavigationIntercepted` indicates whether the navigation was initiated via code or via an HTML navigation. If the `IsNavigationIntercepted` is set to `false`, the navigation was initiated by using the `NavigationManager.NavigateTo` method in the code. If the value of the property is set to `true`, 

```
TODO: Code Sample
```

<br/><br/>


**To create optional route parameters add additional  `@page`  declarations in a component.**

Although there is no specific mechanism for optional route parameters, the functionality can be achieve by using multiple `@page`  declarations.

```
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
<br/><br/>



**Provide a 404 page when the application fails to match a URL to a component**


404 is a standard response code that is returned by a server to indicate that a page was successfully requested but the application was unable to locate it.

```
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

ToDo: Image

<br/><br/>

**Don't use `RedirectToPage` to perform a redirect.**

Do not use the `PageBase.RedirectToPage()` method to perform redirection in Blazer based apps. as `RedirectToPage()` will perform a HTTP redirect to a _Razor_ page. Instead, inject the `NavigationManager` component and use it's `NavigateTo()` method.

```
ToDo: Example
```
<br/><br/>