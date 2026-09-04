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