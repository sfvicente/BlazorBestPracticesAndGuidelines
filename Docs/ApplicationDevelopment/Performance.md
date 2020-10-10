# Application Development | Performance
<br>


### Disable time zones support applications to support the invariant culture if there is no requirement for localization.

A Blazor WebAssembly, by default, includes support for time zones. If not required for the application, you can modify
this behavior. Change the `BlazorEnableTimeZoneSupport` _MSBuild_ property in the application's project file to `false`:

```csharp
<PropertyGroup>
  <BlazorEnableTimeZoneSupport>false</BlazorEnableTimeZoneSupport>
</PropertyGroup>
```

By disabling this feature it won't be include it in the Blazor WebAssembly's runtime, which results in a smaller payload size.

Applies to: Blazor WebAssembly
Additional Tags: Localization, Unused Features
<br>
