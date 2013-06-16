# Fork of msysGit to add support for long path names on Windows

For more details, read [Issue #52](https://github.com/msysgit/msysgit/issues/52)

## First experimental patch

Our company sponsors hackthons for all employees regularly.
These are always great events, where a lot of creative ideas show up and get implemented.

Last time (June, 13th) we've tried to fix issue 52 and adding support for long path names on Windows.

After 21 hours working, we where able to add, commit, status and diff a file with 643 characters long name.
We've tweeted a screenshot [https://twitter.com/nitram509/status/345502581654704128]

See ```issue52-experimental.patch```

Proud, that we've got it done in this pretty short period of time, we know, that we hacked the wrong layer.
The patch changes git core sources directly. Thus it's not worth to ask for a pull request.

But we've learned a lot and want to port the fix into the msys/mingw layer.

[More details will be blogged soon...](http://blog-it.hypoport.de/)

