# Level 0

```bash

# connect remotely with username , hostname and port , will be prompted by password 
ssh bandit0@bandit.labs.overthewire.org -p 2220

#password
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

# Level 1

For special chars use ./

```bash
# for special char like '-' 
cat ./-

# Password 
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

# Level 2

For spaces use backslash

```bash
cat ./--spaces\ in\ this\ filename-- 

7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

# Level 3

```bash
**bandit3@bandit**:**~/inhere**$ ls -a

**.**  **..**  ...Hiding-From-You

**bandit3@bandit**:**~/inhere**$ cat ...Hiding-From-You 

xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

# Level 4
```bash
**bandit4@bandit**:**~/inhere**$ file ./*

./-file00: data

./-file01: data

./-file02: data

./-file03: data

./-file04: data

./-file05: data

./-file06: OpenPGP Public Key

./-file07: ASCII text

./-file08: data

./-file09: Motorola S-Record; binary data in text format

**bandit4@bandit**:**~/inhere**$ cat ./-file07

6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

# Level 5

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

```bash
**bandit5@bandit**:**~/inhere**$ find -type f -size 1033c ! -executable

./maybehere07/.file2

**bandit5@bandit**:**~/inhere**$ cat ./maybehere07/.file2

pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

# Level 6

The password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

```bash
**bandit6@bandit**:**/home**$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

/var/lib/dpkg/info/bandit7.password

**bandit6@bandit**:**/home**$ cat /var/lib/dpkg/info/bandit7.password

Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```


# Level 7

The password for the next level is stored in the file **data.txt** next to the word **millionth**

```bash
**bandit7@bandit**:**~**$ ls

data.txt

**bandit7@bandit**:**~**$ grep millionth data.txt

**millionth** VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

# Level 8

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

```bash
**bandit8@bandit**:**~**$ sort data.txt | uniq -u

EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

# Level 9

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

```bash
**bandit9@bandit**:**~**$ strings data.txt | grep "=="

cL0**==========** the

**==========** password

>**==========** is

R**==========** B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

# Level 10
```shell
**bandit10@bandit**:**~**$ base64 -d data.txt

The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

# Level 11
```shell
**bandit11@bandit**:**~**$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

	The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

# Level 12

The password is in `data.txt`, a hex dump of a file that was compressed repeatedly.

```shell
**bandit12@bandit**:**~**$ cd $(mktemp -d)      # work in a temp dir (home is read-only)
**bandit12@bandit**:**/tmp/tmp.xxx**$ cp ~/data.txt .
**bandit12@bandit**:**/tmp/tmp.xxx**$ xxd -r data.txt data      # undo the hex dump

# Repeat: file <name> -> rename to match -> decompress/extract, until "ASCII text"
$ file data                      # gzip compressed data
$ mv data data.gz && gzip -d data.gz
$ file data                      # bzip2 compressed data
$ mv data data.bz2 && bzip2 -d data.bz2
$ file data.out                  # gzip compressed data
$ mv data.out data.gz && gzip -d data.gz
$ file data                      # POSIX tar archive
$ tar -xf data                   # -> new file (e.g. data5.bin)
$ file data5.bin                 # POSIX tar archive
$ tar -xf data5.bin              # -> data6.bin
$ file data6.bin                 # bzip2 compressed data
$ bzip2 -d data6.bin             # -> data6.bin.out
$ file data6.bin.out             # POSIX tar archive
$ tar -xf data6.bin.out          # -> data8.bin
$ file data8.bin                 # gzip compressed data
$ mv data8.bin data8.gz && gzip -d data8.gz
$ file data8                     # ASCII text
$ cat data8

The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```