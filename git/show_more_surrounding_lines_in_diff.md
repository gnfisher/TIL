# Show more surrounding lines in diff

I've been working in Scala the last 18-months and often to understand a change
I'll need more context than the +3,-3 lines of context that `git diff` defaults
to.

You can pass a `-U` or `--unified=` flag to `diff` to tell it to show more:

`git diff -U10` would show +10,-10 lines around the diff in question.
