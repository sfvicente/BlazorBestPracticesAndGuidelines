# Components | Security
<br>

## Content Rendering
<br> 


### Don't render raw HTML constructed from any untrusted source

Rendering raw HTML from sources that you do not trust is a security risk and should be avoided. Instead, use built-in
mechanisms or third-party libraries for HTML sanitization.

```csharp
@inject IHtmlSanitizer HtmlSanitizer

@if (!string.IsNullOrEmpty(UntrustedHtml))
{
    <div>
        @HtmlSanitizer.Sanitize(UntrustedHtml)
    </div>
}
else
{
    <p>No content available.</p>
}

@code {
    // Simulated untrusted HTML content
    string UntrustedHtml = "<script>alert('This is a malicious script!');</script>";
}
```

Additional Tags: Rendering
<br><br>


## Navigation
<br>


### Avoid using user input as part of the navigation call arguments.

```csharp
// ToDo: Example
```

Additional Tags: User Input, Navigation
<br><br>


### Always validate component arguments to ensure that the target for navigation requests is allowed by the app.

Although it should be avoided, in case the application uses user input as part of the navigation logic, before executing the `NavigationManager.NavigateTo()` method,
the inputs need to be properly validated. Otherwise, the application may be redirected to a malicious site.

```csharp
// ToDo: Example
```

Additional Tags: Navigation
<br><br>


## Link Rendering
<br>

### When rendering links as part of an application, if possible, use relative links.

```csharp
// ToDo: Example
```
<br><br>


### When rendering links as part of an application, validate that absolute link destinations are valid before including them in a page.

```csharp
// ToDo: Example
```
<br><br>