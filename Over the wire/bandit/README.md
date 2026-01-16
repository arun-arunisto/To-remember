Machine: Kali Linux

### Level 0

To ssh into a system, use the following command:
```
ssh <username>@<host> -p <port>
```

### Level 1 -> 2

To read `-` this file `cat -` this command won't work, so you need to use the following:
```
cat ./-
```

### Level 2 -> 3
To read `--spaces in this filename--` this file `cat ./--spaces in this filename--` this won't work, you need to add quotes also:
```
cat ./"--spaces in this filename--"
```

### Level 3 -> 4
To find the hidden files, use the following command:
```
ls -a
```

### Level 4 -> 5
There will be more than 10 files, and in one of these files, the password is saved as 'ASCII Text.' We need to find that:
```
ls -la
```
The above command will print all the files:
```
file ./*
```
Use this to find the content type


### Level 5 -> 6

HINTS: 

Human-readable

1033 bytes

not executable

---
- Human-readable

```
file */{.,}* | grep "ASCII text" | grep -v ', with very long lines'
```

- 1033 bytes

```
du -b -a | grep 1033
```
### Level 6 -> 7

HINTS:

owned by user bandit7

owned by group bandit6

33 bytes in size

```
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
The above command covered all the hints

### Level 7 -> 8

```
cat data.txt | grep millionth
```
