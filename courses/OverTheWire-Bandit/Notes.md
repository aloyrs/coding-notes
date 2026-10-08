# Terminal Cheat Sheet (from OverTheWire Bandit)

Commands and the file types they act on. Scope: what a full-stack dev / home-server admin (Unraid, Docker, PostgreSQL) actually uses. Stopping point is Bandit **Level 15**; sections marked **[not in Bandit]** fill gaps the wargame never covers.

## Contents

1. [Mental model: streams, pipes, quoting](#1-mental-model-streams-pipes-quoting)
2. [Navigate and read](#2-navigate-and-read)
3. [Identify file types](#3-identify-file-types)
4. [Find files](#4-find-files)
5. [Search and transform text](#5-search-and-transform-text)
6. [Encoding and binary](#6-encoding-and-binary)
7. [Archives and compression](#7-archives-and-compression)
8. [SSH, keys, and ports (Levels 13-15)](#8-ssh-keys-and-ports-levels-13-15)
9. [Permissions and processes [not in Bandit]](#9-permissions-and-processes-not-in-bandit)
10. [Daily-driver extras [not in Bandit]](#10-daily-driver-extras-not-in-bandit)
11. [Recipes](#11-recipes)

---

## 1. Mental model: streams, pipes, quoting

| Number | Name | Carries |
| --- | --- | --- |
| `0` | stdin | Input |
| `1` | stdout | Normal output |
| `2` | stderr | Errors |

```bash
cmd > out.txt          # stdout to file (overwrite)
cmd >> out.txt         # stdout to file (append)
cmd 2>/dev/null        # discard errors (e.g. "Permission denied" noise from find /)
cmd > out.txt 2>&1     # stdout + stderr to the same file
cmd1 | cmd2            # feed stdout of cmd1 into stdin of cmd2
cmd1 && cmd2           # run cmd2 only if cmd1 succeeded
cd $(mktemp -d)        # $(...) = substitute the command's output; here, a scratch dir
```

**Awkward filenames** (Levels 1-3):

| Problem | Fix |
| --- | --- |
| Name starts with `-` (read as a flag) | `cat ./-file` or `cat -- -file` |
| Spaces in name | `cat "my file"` or `cat my\ file` |
| Hidden (starts with `.`) | `ls -a` |

---

## 2. Navigate and read

```bash
ls -lah               # long + hidden + human sizes (the one you want)
cd -                  # back to previous directory
cat f                 # print file
cat -n f              # with line numbers
less f                # scroll a big file (q quits, /text searches)
head -n 20 f          # first 20 lines
tail -n 50 f          # last 50 lines
tail -f f             # follow a growing file (live logs)  [not in Bandit]
wc -l f               # count lines  [not in Bandit]
du -sh *              # size of each item here
du -sh * | sort -h    # ...largest last
df -h                 # free space per disk/mount  [not in Bandit]
```

---

## 3. Identify file types

`file` reads the **magic bytes**, not the extension. Trust it over the filename.

```bash
file f        # what is this really?
file ./*      # check a whole directory (Level 4)
```

| `file` output | What it is | Open / use with |
| --- | --- | --- |
| `ASCII text`, `UTF-8 text` | Plain text (logs, `.env`, configs, JSON, SQL) | `cat`, `less`, `grep` |
| `data` | Unknown/binary blob | `xxd`, `strings` |
| `gzip compressed data` | `.gz` | `gzip -d`, `zcat` |
| `bzip2 compressed data` | `.bz2` | `bzip2 -d`, `bzcat` |
| `POSIX tar archive` | `.tar` | `tar -xf` |
| `Zip archive data` | `.zip` | `unzip` |
| `ELF 64-bit executable` | Compiled Linux binary | `strings`, run it |
| `OpenSSH private key` / `PEM RSA private key` | SSH identity (`id_rsa`) | `ssh -i`, needs `chmod 600` |
| `OpenPGP Public Key` | GPG key | `gpg` |
| `Motorola S-Record` | Firmware-style hex text | `xxd -r` |
| `symbolic link to X` | Symlink | `readlink -f f` |

---

## 4. Find files

```bash
find . -name "*.log"                     # by name (quote the glob)
find . -type f -size 1033c               # regular file, exactly 1033 bytes
find . -type f -size +100M               # bigger than 100 MB  [not in Bandit]
find . -type f -not -executable          # NOT executable (same as ! -executable)
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
find . -mtime -1                         # modified in last day  [not in Bandit]
find . -name "*.log" -delete             # careful: deletes matches  [not in Bandit]
find . -name "*.tmp" -exec rm {} +       # run a command on each match  [not in Bandit]
```

| Filter | Meaning |
| --- | --- |
| `-type f` / `-type d` | file / directory |
| `-name` / `-iname` | name glob (case-sens / insens) |
| `-size 33c` `+1M` `-10k` | `c` bytes, `k`, `M`, `G`; `+` bigger, `-` smaller |
| `-user` `-group` | owner / group |
| `-perm 644` | exact permission bits |
| `-executable` | executable by you |

Always start from `.` or a path. Searching `/` needs `2>/dev/null`.

---

## 5. Search and transform text

### `grep`

```bash
grep "millionth" data.txt      # lines containing it
grep -i err app.log            # case-insensitive
grep -rn "TODO" .              # recursive, with filename:line
grep -v "DEBUG" app.log        # invert: lines NOT matching
grep -E "error|fatal" app.log  # regex alternation
grep -C 3 "exception" app.log  # 3 lines of context around matches
```

### `sort` / `uniq` (uniq only sees **adjacent** lines, so sort first)

```bash
sort f                    # alphabetical
sort -n f                 # numeric
sort -r f                 # reverse
sort f | uniq             # dedupe
sort f | uniq -u          # lines that appear exactly once (Level 8)
sort f | uniq -c | sort -rn | head   # top-N most frequent lines
```

### `tr` (stdin only)

```bash
cat f | tr 'a-z' 'A-Z'                 # uppercase
cat f | tr -d '\r'                     # strip Windows line endings
cat f | tr 'A-Za-z' 'N-ZA-Mn-za-m'     # ROT13 (Level 11)
```

### `cut`, `awk`, `sed`, `xargs`  **[not in Bandit, but daily use]**

```bash
cut -d',' -f2 data.csv           # 2nd comma-separated column
awk '{print $1, $NF}' f          # first and last whitespace-separated field
awk -F: '{print $1}' /etc/passwd # custom delimiter
sed 's/old/new/g' f              # substitute (prints result)
sed -i 's/old/new/g' f           # edit in place (macOS needs: sed -i '' ...)
cmd | xargs -n1 echo             # turn lines into arguments
```

### `jq` for JSON  **[not in Bandit; install it]**

```bash
curl -s api/url | jq .                  # pretty-print
curl -s api/url | jq '.items[].name'    # pluck fields
docker inspect ctr | jq '.[0].Mounts'
```

---

## 6. Encoding and binary

```bash
strings data.bin | grep "=="     # readable text inside a binary (Level 9)
strings -n 8 data.bin            # only strings >= 8 chars

base64 file > file.b64           # encode
base64 -d file.b64               # decode (Level 10). JWT/API payloads are base64
echo 'dGVzdA==' | base64 -d      # decode a string

xxd file | head                  # hex + ASCII view
xxd -r hex.txt > out.bin         # reverse a hex dump to binary (Level 12)
```

| Input file | Tool |
| --- | --- |
| Binary with some text inside | `strings` |
| Base64 text (`...==`) | `base64 -d` |
| Hex dump text | `xxd -r` |
| ROT13 text | `tr` |

---

## 7. Archives and compression

| Extension | Made by | Undo with |
| --- | --- | --- |
| `.tar` | `tar -cf` | `tar -xf` |
| `.gz` | `gzip` | `gzip -d` |
| `.bz2` | `bzip2` | `bzip2 -d` |
| `.tar.gz` / `.tgz` | `tar -czf` | `tar -xzf` |
| `.tar.bz2` | `tar -cjf` | `tar -xjf` |
| `.zip` | `zip -r` | `unzip` |

```bash
tar -czf backup.tar.gz dir/      # create a gzipped archive
tar -xzf backup.tar.gz           # extract
tar -xzf backup.tar.gz -C /dest  # extract into a directory
tar -tzf backup.tar.gz           # list contents without extracting
gzip -d f.gz                     # decompress (needs .gz name)
bzip2 -d f.bz2                   # decompress (output keeps name minus .bz2)
zip -r out.zip dir/ ; unzip out.zip
```

**Level 12 loop** (repeatedly compressed file): work in `cd $(mktemp -d)`, `xxd -r data.txt data`, then repeat **`file` -> rename to match -> decompress** until `ASCII text`.

| `file` says | Do |
| --- | --- |
| gzip | `mv f f.gz && gzip -d f.gz` |
| bzip2 | `mv f f.bz2 && bzip2 -d f.bz2` |
| POSIX tar | `tar -xf f` (creates a NEW file; continue with that one) |
| ASCII text | `cat f`, done |

Gotchas: `gzip -d` refuses a name without `.gz`; `tar -xf` leaves the old archive behind, so `ls` to spot the new file.

---

## 8. SSH, keys, and ports (Levels 13-15)

*Not yet done in the wargame. Commands below are from the level goals, not your own solves.*

```bash
ssh user@host -p 2220                    # connect on a non-default port (Level 0)
ssh -i ~/.ssh/id_rsa user@host           # log in with a private key (Level 13)
ssh user@host 'ls /var/log'              # run one command remotely, then exit
scp file user@host:/path/                # copy to remote  [not in Bandit]
scp user@host:/path/file .               # copy from remote
ssh-keygen -t ed25519                    # make a key pair  [not in Bandit]
ssh-copy-id user@host                    # install your public key  [not in Bandit]
```

**Key files:** private key = `id_rsa` / `id_ed25519` (never share); public key = `.pub`; allowed keys on the server = `~/.ssh/authorized_keys`. SSH **refuses a private key that is readable by others**:

```bash
chmod 600 ~/.ssh/id_rsa
```

**Talking to a port** (Level 14):

```bash
nc localhost 30000                       # open a raw TCP connection, type input
echo "secret" | nc localhost 30000       # pipe a string into a port
nc -zv host 5432                         # is the port open? (Postgres check)  [not in Bandit]
```

**Talking to a TLS port** (Level 15; `nc` can't do TLS):

```bash
openssl s_client -connect localhost:30001      # TLS client; type/pipe your input
echo "secret" | openssl s_client -connect localhost:30001 -quiet
```

Passwords for the next level live in `/etc/bandit_pass/banditN` (readable only by that user).

---

## 9. Permissions and processes [not in Bandit]

Bandit only *reads* permissions (`find -user`, `ls -l`). You also need to change them.

```bash
ls -l f
# -rwxr-xr--  1 owner group ...
#  |\_/\_/\_/   r=4 w=2 x=1 for owner / group / others

chmod 600 f              # owner rw only (SSH keys, .env)
chmod 644 f              # owner rw, others read
chmod 755 f              # executable script/dir
chmod +x script.sh       # make executable
chown user:group f       # change owner (needs sudo)
chown -R 99:100 dir/     # Unraid default appdata owner is nobody:users
sudo cmd                 # run as root
```

```bash
ps aux | grep nginx      # find a process
top    # or htop         # live CPU/RAM
kill PID ; kill -9 PID   # stop (polite / force)
ss -tulpn                # what is listening on which port (netstat replacement)
lsof -i :5432            # who owns port 5432
journalctl -u docker -f  # service logs (systemd distros; Unraid uses /var/log/syslog)
```

---

## 10. Daily-driver extras [not in Bandit]

```bash
# Docker
docker ps -a                       # containers
docker logs -f --tail 100 ctr      # follow logs
docker exec -it ctr sh             # shell inside container
docker inspect ctr                 # volumes, env, networks (pipe to jq)
docker compose up -d / down / logs -f

# PostgreSQL
psql -h host -U user -d db         # connect
psql -c "SELECT now();"            # one-off query
pg_dump -U user db > db.sql        # backup (a plain SQL text file)
psql -U user db < db.sql           # restore

# HTTP
curl -s url                        # GET
curl -i url                        # include headers
curl -X POST -H "Content-Type: application/json" -d '{"a":1}' url

# Sessions and scheduling
tmux new -s main ; tmux attach -t main   # session survives disconnects
crontab -e                               # schedule jobs (min hour dom mon dow cmd)
rsync -avh --progress src/ user@host:dst/   # smarter copy than scp
```

---

## 11. Recipes

```bash
# Top 10 IPs in an access log
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head

# Errors in the last 1000 lines
tail -n 1000 app.log | grep -i error

# Find big files hogging space
du -sh * | sort -h | tail

# Find where a string is used in a project
grep -rn "DATABASE_URL" . --include="*.env*" --include="*.yml"

# Peel a stack of compressed layers
file f   # then gzip -d / bzip2 -d / tar -xf as `file` dictates, repeat
```
