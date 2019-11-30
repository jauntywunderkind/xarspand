# xarspand

> xargs ⨯ eval shell tool

for each line of input, run a program/pipeline, and output each input+output line pair.

xarspand was created because the author observed that many unix operations like sorting work with columnarized data, yet there were not good tools to take existing columnar data, run it through a pipeline, and produce more columnar data.

# examples

## names-length

for a list of names, let's add a column with the number of characters:

```
$ echo -n "julie\njohn\njane" | xarspand 'echo -n % | wc -c'
julie 5
john 4
jo 2
```

## first name length

we could also extract the length of only a first name, by putting awk into our pipeline:

```
$ echo -n "jackson jamis\njohnny jojack\njillie jigon" | xarspand "echo -n % | awk '{print $1}' | wc -c"
jackson jamis 8
johnny jojack 7
jillie jigon 7
```

## pivot

a program that produces more than one line of output will produce a row of output for each line:

```
$ echo -n "jacklyn\njames\njo" | xarspand 'echo -n % | wc -c ; echo -n %%% | wc -c'
jacklyn 7
jacklyn 21
james 5
james 15
jo 2
jo 6
```

## text processing

the input line can be suppressed via a XARSPAND_PREFIX=false statement:

```
$ echo -n "jimmy\njamie\njackie\n" | XARSPAND_PREFIX=false xarspand echo -n '"hi %,\nhow are you?\n\n"'
hi jimmy,
how are you?

hi jamie,
how are you?

hi jackie,
how are you?
```
