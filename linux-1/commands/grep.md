# grep

[https://www.howtoforge.com/tutorial/linux-grep-command/](https://www.howtoforge.com/tutorial/linux-grep-command/)

the basic syntax:

```bash
grep 'word' filename
grep 'word' file1 file2 file3
grep 'string1 string2'  filename
cat otherfile | grep 'something'
command | grep 'something'
command option1 | grep 'data'
grep --color 'data' fileName
grep [-options] pattern filename
```

recursive search:

```bash
grep -r "mydomain.com" /etc/apache2/
```
