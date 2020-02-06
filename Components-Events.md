# Components | Events
<br>

Use the @on{EVENT}:stopPropagation directive attribute to stop event propagation.

```
<input type="text" value="" @onkeypress:preventDefault />
```

<br/><br/>

Use both the @on{EVENT}:stopPropagation directive attribute and with your event handling to stop event propagation but still process your code.

```
<input type="text" value="" @onkeypress="HandleKeyPresses" @onkeypress:preventDefault />
```




