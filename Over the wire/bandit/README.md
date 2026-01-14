Machine: Kali Linux

### Level 0

To ssh into a system, use the following command:
```
ssh <username>@<host> -p <port>
```

### Level 2

To read `-` this file `cat -` this command won't work, so you need to use the following:
```
cat ./-
```

### Level 3
To read `--spaces in this filename--` this file `cat ./--spaces in this filename--` this won't work, you need to add quotes also:
```
cat ./"--spaces in this filename--"
```

### Level 4
To find the hidden files, use the following command:
```
ls -a
```
