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

### Level 5
There will be more than 10 files, and in one file password is saved as 'ASCII Text.' We need to find that:
```
ls -la
```
The above command will print all the files:
```
file ./*
```
Use this to find the content type
