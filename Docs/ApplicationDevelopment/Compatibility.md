# Application Development | Compatibility
<br>


### Add `browser` as a supported platform in the project file to enable browser compatibilty checks for libraries.

```csharp
<SupportedPlatform Include="browser" />
```

This is not required for Blazor WebAssembly projects and Razor class library projects as it is added automatically.

<sub>Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/</sub>
<br><br>


### Use the `UnsupportedOSPlatform` attribute to indicate that a specific API is not supported in browsers.

When authoring a library, you can optionally indicate that a particular API is not supported in browsers by applying the UnsupportedOSPlatformAttribute:

```csharp
[UnsupportedOSPlatform("browser")]
private static string GetLoggingDirectory()
{
    // ...
}
```

<sub>Reference: https://devblogs.microsoft.com/aspnet/asp-net-core-updates-in-net-5-release-candidate-1/</sub>
<br><br>


### Use a conditional `Microsoft.AspNetCore.Components` package reference to support both .NET Core 3.x and .NET 5.

// todo: complement description

Microsoft recommends the following:

```xml
<PackageReference Include="Microsoft.AspNetCore.Components" Version="3.0.0" Condition="'$(TargetFramework)' == 'netstandard2.0'" />

<PackageReference Include="Microsoft.AspNetCore.Components" Version="5.0.0-rc.1.*" Condition="'$(TargetFramework)' != 'netstandard2.0'" />
```

<br><br>

