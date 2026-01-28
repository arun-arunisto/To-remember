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

### Level 8 -> 9

```
sort data.txt | uniq -u
```

### Level 9 -> 10
```
strings data.txt | grep ===
```
### Level 10 -> 11
To decode base64
```
base64 -d data.txt
```
### Level 11 -> 12
```
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
### Level 12 -> 13
```
https://mayadevbe.me/posts/overthewire/bandit/level13/
```
### Level 13 -> 14
used `scp` to transfer the data over the network to the remote
``` syntax
scp -P <port> <user>@<IP>:<remotefilepath> <localfilepath>
```
Actual code
```
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```
Then we used the `ssh` command to access the next level.
```
ssh -i <ssh_privete_key> <user>@<host> -p <port>
```
before that use `chmod 700 sshkey.private` to accessible

### Level 14 -> 15
In the previous level they mentioned the password in the `/etc/bandit_pass/bnadit14`, so run the following command to retrieve the password:
```
cat /etc/bandit_pass/bandit14
```
then used `nc` or `netcat` to communicate over the network:
``` syntax
nc <host> <port>
```
the actual command is:
```
nc localhost 30000
```
and put the password that we got from the `/etc/`.

### Level 15 -> 16
Use the `openssl` to connect with the localhost and the syntax is:
```
openssl s_client <host>:<port>
```
```
openssl s_client localhost:30001
```
then paste the password of bandit15
