# Miscellaneous issues

This is a place to record experience: issues we've had and things that have
worked well that don't fit anywhere else in particular in the documentation.

## Clean up your garbage

Images are very large. By default, if you don't free the memory of a `Mat`,
it'll stay in memory for an indefinite time until Java cleans it up (frees it).
This is a memory leak.

In 2016, a few times we demoed CV, repeatedly running the routine to aim and
shoot. After 20-30min of this, we'd get a `java.lang.OutOfMemoryError`. This
never happened in a match (which is of course much shorter).

The consequence: the code unconditionally crashes. Don't try to
catch this kind of error. (There's a reason some errors in Java
are `Error`s and not `Exception`s: `Error`s cannot be recovered
from.)

### The solution

Call the `.release()` method of `Mat`s when you are done
with them.

(When possible, also overwrite previous `Mat`s instead of creating new ones.
This also helps performance.)
