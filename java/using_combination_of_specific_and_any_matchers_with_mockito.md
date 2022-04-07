# When you want to match parameters but not all of them!

When you use Mockito Argument Matchers like `anyInt()`, if you use one, all arguments must be matchers.

If only want one of the arguments to be nonspecific, you can wrap the specific ones in `eq()`.

```java
when(someClass.doesThing(eq(true), anyInt()).thenReturn(true);
```

See also: [Mockito Argument Matchers](https://www.journaldev.com/21876/mockito-argument-matchers-any-eq)
