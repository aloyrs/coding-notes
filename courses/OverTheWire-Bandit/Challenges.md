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

```bash
**bandit5@bandit**:**~/inhere**$ find -type f -size 1033c ! -executable

./maybehere07/.file2

**bandit5@bandit**:**~/inhere**$ cat ./maybehere07/.file2

pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```