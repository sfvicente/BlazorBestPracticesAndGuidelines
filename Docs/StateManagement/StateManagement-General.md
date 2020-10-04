# State Management | General
<br>


### Prefer `sessionStorage` to `localStorage` to store transient application data and avoid synchronization across multiple browser tabs.

If you want to avoid performing synchronization state across browser tags, it is generaly safer to use `sessionStorage` as it is scope to the current browser tab.

TODO: complement.

<br>


**Use custom code to persist UI state.**

User interface state can't be persisted in a similar way to component instances and their render trees. To persist something similar to UI state, such as the expanded nodes of a TreeView, the app must have custom code to model the behavior as serializable app state.

```csharp
TODO: Example
```
<br><br>
