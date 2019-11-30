# xarspand

> map stdin through another program, producing a table of output

# example

```
$ echo -n "julie\njohn\njane\n" | xarspand echo -n '"hi %, how are you"' '|' wc -c
julie 21
john 20
jane 20
```

# comple example

```
$ echo -n "jimmy\njamie\njackie\n" | XARSPAND_PREFIX=false xarspand echo -n '"hi %,\nhow are you?\n\n"'
hi jimmy,
how are you?

hi john,
how are you?

hi jane,
how are you?

```
