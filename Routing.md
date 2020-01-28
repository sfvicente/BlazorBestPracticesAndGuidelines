# Routing



**Use the `LocationChanged` event to determine when the URL in the browser is changed.**

`LocationChanged` is an event that is triggered whenever the URL in the browser is modified. It passes an instance of `LocationChangedEventArgs` which provides the the URL :

```
Example
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