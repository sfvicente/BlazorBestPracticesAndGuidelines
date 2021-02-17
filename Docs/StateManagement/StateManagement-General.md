# State Management | General
<br>


## Browser Storage

Browser storage, also known as local storage or web storage is a feature that allows web applications to store information on a user's browser. It provides an alternative solution
to cookies. HTML5 provides the `localStorage` and the `sessionStorage` objects for storing and manipulating data on the browser.
<br>


### Prefer `sessionStorage` to `localStorage` to store transient application data and avoid synchronization across multiple browser tabs.

If you want to avoid performing synchronization state across browser tags, it is generaly safer to use `sessionStorage`. As `sessionStorage` is scope to the current browser tab,
it avoids bugs when managing state across tags and conflicting behavior if state is overwritten by performing actions on other tabs.

TODO: complement.

<br>


### Use the browsers local storage to persist application state across closing and re-opening the browser.

The `localStorage` collection is scoped to the browser's window. The stored application state will be persisted even if the user reloads the page or closes and re-opens the browser.

TODO: complement.
<br>


### Use the `ProtectedLocalStorage` in a component that requires loading or saving data to the browser's local storage.

The `ProtectedLocalStorage` class allows storing and retrieving data in the browser's local storage collection. Any data stored through this method, will be shared across all tabs. The
data will also be persisted even if the browser is restarted.

Use the `@inject` directive to inject an instance of `ProtectedLocalStorage` in a component:

```csharp
@using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage
@inject ProtectedLocalStorage ProtectedLocalStore
```

// TODO: Complement description
// TODO: add code samples

Applies To: Blazor Server
<br>


### Use the `ProtectedSessionStorage` in a component that requires loading or saving data to the browser's session storage collection.

The `ProtectedSessionStorage` class allows storing and retrieving data in the browser's session storage collection. Any data stored through this method, will be scoped
to the current browser tab. If the user closes the browser tab or the browser application, all the data will be discarded.

Use the `@inject` directive to inject an instance of `ProtectedSessionStorage` in a component. Call the `SetAsync` method to store the data in the session storage:

```csharp
@using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage
@inject ProtectedSessionStorage ProtectedSessionStore

...

@code
{
    protected override async Task OnInitializedAsync()
    {
        await protectedSessionStorage.SetAsync("userSetting", mySetting);
    }
}
```

To read previously saved data, use the `GetAsync` method:

```csharp
@using Microsoft.AspNetCore.Components.Server.ProtectedBrowserStorage
@inject ProtectedSessionStorage protectedSessionStorage

...

@code
{
    protected override async Task OnInitializedAsync()
    {
        ProtectedBrowserStorageResult<string> userSettingStorageResult = await protectedSessionStorage.GetAsync<string>("userSetting");

        if (userSettingStorageResult.Success)
        {
            string userSetting = userSettingStorageResult.Value;

            ...
        }

        ...
    }
}
```

Applies To: Blazor Server
<br>


## Data Persistence
<br>


### Use custom code to persist UI state.

User interface state can't be persisted in a similar way to component instances and their render trees. To persist something similar to UI state, such as the expanded nodes of a TreeView, the app must have custom code to model the behavior as serializable app state.

```csharp
TODO: Example
```
<br><br>


### Always use a server-side database to store permanent data or data that is required to cross multiple users or devices.

TODO: complement description

The options for server-side databases include:
    - Relational SQL database
    - NoSQL database
    - Key-value store
    - Blob store

<br>