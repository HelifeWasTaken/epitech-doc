# GetNextLine

Write a function that will store, in the parameter "line", a line that has been
read from the given file descriptor.

## How it should work

Calling your function GetNextLine in a loop will therefore allow you to read
the text available on a file descriptor one line at a time until the end of the
text, no matter the size of either the text or one of its lines. Therfore, make
sure that your function behaves well when it reads from a file, from the
standard output, from a redirection etc. For the mandatory part, no call to
another function will be done on the file descriptor between 2 calls of
GetNextLine.

Finally we consider that GetNextLine has an undefined behavior when reading
from a binary file. You may make this work accordingly, but its not part of the
bonus nor is it required.

## The basics:

You should know about pointer manipulation and pointer arithmetics

If you know what means considering a `char *s = "hello"`:
```c
char *s2 = s + 5
char c = *(s + 3)
char c2 = s[2]
char *s3 = &s[4]
char *s4 = s++ // This one is REALLY tricky
char *s5 = ++s // This one too
char c3 = *++s // and the other too
char s6 = *(++s + 4) // Lmao you can understand that you basically understand pointer arithmetic
char s7 = *(s++ + 4) // And now you understand the diff between s++ and ++s totally
```
Then now you are good to go

Therefore it is also required to know how the static keyword and it's meaning on variable it is not the same on a function
(A simple introduction to the static variables)[https://www.geeksforgeeks.org/static-variables-in-c/]

Make sure to read well what are required in your project the things listed above are maybe outadated so don't take them too seriously
