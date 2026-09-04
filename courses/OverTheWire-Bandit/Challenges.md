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

**How It Works**

- `/`: Searches the entire filesystem from the root directory down.
    
- `-user bandit7`: Filters for files owned by user `bandit7`.
    
- `-group bandit6`: Filters for files owned by group `bandit6`.
    
- `-size 33c`: Restricts results to files that are exactly 33 bytes (`c` = bytes).
    
- `2>/dev/null`: Redirects standard error (stderr) to `/dev/null`, muting all "Permission denied" messages so only the matching file path is printed.

# Level 7

