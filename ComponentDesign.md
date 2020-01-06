# Component Design




### Usage of the  `@key`

**CS010 - Use `@key` whenever a list such as a `@foreach` block is rendered and a suitable value exists to define the `@key`.**

>example

**CS011 - Use `@key` to prevent Blazor from preserving an element or component subtree when an object changes**

>example

**CD0xx - Do not to use @key when there's a performance cost when diffing with  `@key`.**

>example
>
The performance cost isn't large, but only specify  `@key`  if controlling the element or component preservation rules benefit the app.


**CS012 - Only use distinct values, such as object instances or primary key values**

>example