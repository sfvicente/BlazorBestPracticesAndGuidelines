# Application Development | Compatibility
<br>


### Use the `UnsupportedOSPlatform` attribute to indicate that a specific API is not supported in browsers.

When authoring a library, you can optionally indicate that a particular API is not supported in browsers by applying the UnsupportedOSPlatformAttribute:

```csharp
[UnsupportedOSPlatform("browser")]
private static string GetLoggingDirectory()
{
    // ...
}
```

Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/

