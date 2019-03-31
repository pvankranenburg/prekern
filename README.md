# prekern

prekern was written to assist with the encoding of musical scores into **kern files. It's a preprocessor for **kern. It adds some context-dependency to the symbols. prekern takes a file with a single spine in context-dependent notation as input and outputs a file with the spine in **kern format.

prekern translates line by line into **kern format. The information that is not explicitly entered is "inherited" from the previous line.

The following rules apply:

- A line containing "**prekern" will be translated into a line with "**kern".
- A line starting with '!', '*' or '=' will just be copied.
- A line starting with '%' will be copied without the leading '%'. Thus the converting mechanism can be escaped.
- If the pitch is preceded by a '@', the **kern interpretation is used to determine the octave. This should be used for the first note in the spine, and can be used for any subsequent note.
- If for a certain note the duration is not provided, the duration of the preceding note is used.
- If for a certain note the octave information is not provided, the note is taken that is nearest to the previous note (i.e. within a fifth).
- If a note is a fifth or more from the previous note, either '@' followed by the **kern representation or one of the signs '>' (an octave higher) and '<' (an octave lower) should be used.
- The canonical order of **kern signifiers must be used.

An example to make things clear:

input: example.pk	output: example.krn

```**prekern       **kern
*MM76           *MM76
*k[b-]          *k[b-]
*M4/4           *M4/4
=1              =1
4@cc            4cc
d               4dd
e               4ee
8f              8ff
g               8gg
=2              =2
2a<             2a
16b-            16b-
c               16cc
d               16dd
e               16ee
%16FFF          16FFF
g               16gg
a               16aa
d<              16dd
=3              =3
4@DD            4DD
e               4EE
f @G @b-        4FF 4G 4b-
e a c           4EE 4A 4cc
==              ==
*-              *-
```

To compile, put prekern.cc and prekern.h in the same directory and enter something like:

`g++ -o prekern prekern.cc`

on the command line, if you're using the GNU Compiler Collection. With other compilers, you're on your own.
I provide this because it is helpful for me and it might be helpful for others. It is not under active development. Prekern is released under the GPL.
