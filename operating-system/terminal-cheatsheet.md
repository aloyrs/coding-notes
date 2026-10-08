# Terminal Cheat Sheet

Everything a full-stack dev / home-server admin (Unraid, Docker, PostgreSQL) needs. Each section: **command → what it does → when to reach for it**. Scan the "I want to..." table first.

## I want to... (jump table)

| I want to...                       | Use                                | Section                          |
| ---------------------------------- | ---------------------------------- | -------------------------------- |
| Move around, see what's here       | `ls -lah`, `cd`, `pwd`             | [1](#1-navigate--manage-files)   |
| Copy / move / delete / make files  | `cp`, `mv`, `rm`, `mkdir`, `touch` | [1](#1-navigate--manage-files)   |
| Read a file or a log               | `cat`, `less`, `head`, `tail -f`   | [2](#2-read-files)               |
| Know what a mystery file really is | `file`, `strings`, `xxd`           | [3](#3-identify--inspect-files)  |
| Find a file by name/size/owner     | `find`                             | [4](#4-find-files)               |
| Find text inside files             | `grep -rn`                         | [5](#5-search-and-reshape-text)  |
| Slice columns / count / dedupe     | `awk`, `cut`, `sort`, `uniq`, `wc` | [5](#5-search-and-reshape-text)  |
| Edit a file in place               | `sed -i`, `nano`, `vim`            | [5](#5-search-and-reshape-text)  |
| Pretty-print / query JSON          | `jq`                               | [5](#5-search-and-reshape-text)  |
| Compress / extract                 | `tar`, `gzip`, `zip`               | [6](#6-archives--compression)    |
| Fix "permission denied"            | `chmod`, `chown`, `sudo`           | [7](#7-permissions-and-users)    |
| See / kill what's running          | `ps`, `top`, `kill`, `ss`, `lsof`  | [8](#8-processes--system-health) |
| Check disk / RAM                   | `df -h`, `du -sh`, `free -h`       | [8](#8-processes--system-health) |
| Hit an API / download              | `curl`, `wget`                     | [9](#9-network)                  |
| Log into / copy to a server        | `ssh`, `scp`, `rsync`              | [10](#10-remote-access-ssh)      |
| Work with containers               | `docker`, `docker compose`         | [11](#11-docker)                 |
| Work with the database             | `psql`, `pg_dump`                  | [12](#12-postgresql)             |
| Keep a session alive / schedule    | `tmux`, `crontab`                  | [13](#13-sessions--scheduling)   |
| Chain commands together            | `\|`, `>`, `&&`, `$(...)`          | [0](#0-core-concepts)            |

---

## 0. Core concepts

```bash
cmd1 | cmd2          # pipe: stdout of cmd1 becomes stdin of cmd2
cmd > f              # stdout to file (overwrite)      cmd >> f   append
cmd 2>/dev/null      # throw away errors (noisy find /)
cmd > f 2>&1         # stdout + errors to same file
cmd1 && cmd2         # run cmd2 only if cmd1 succeeded
cmd1 ; cmd2          # run both regardless
cd $(mktemp -d)      # $(...) = use a command's output; here a scratch dir
```

| Streams | `0` stdin | `1` stdout | `2` stderr |
| --- | --- | --- | --- |

**Awkward filenames:** starts with `-` → `cat ./-file` · has spaces → `cat "my file"` · hidden (dot-file) → `ls -a`.
**Help:** `man cmd`, `cmd --help`, `tldr cmd` (if installed). **Cancel:** `Ctrl+C`. **Search history:** `Ctrl+R`.

---

## 1. Navigate & manage files

| Command | Does | Use when |
| --- | --- | --- |
| `pwd` | Print current dir | You're lost |
| `ls -lah` | Long list, hidden files, human sizes | Default way to look around |
| `cd dir` / `cd ..` / `cd -` / `cd ~` | Go to dir / up / previous / home | Moving |
| `mkdir -p a/b/c` | Make dirs (and parents) | New project/folder |
| `touch f` | Create empty file / update timestamp | Quick placeholder |
| `cp -r src dst` | Copy (`-r` for dirs) | Backup before editing |
| `mv src dst` | Move **or rename** | Reorganising |
| `rm f` / `rm -r dir` | Delete file / dir tree | **No trash. `rm -rf` is permanent; check the path first** |
| `ln -s target link` | Symlink | Point config to a shared location |
| `tree -L 2` | Directory tree | Understand a project layout |

---

## 2. Read files

| Command | Does | Use when |
| --- | --- | --- |
| `cat f` | Print whole file | Short files, `.env`, configs |
| `less f` | Scroll (`/text` search, `q` quit, `G` end) | Big files and logs |
| `head -n 20 f` / `tail -n 50 f` | First / last N lines | Peek at CSV header / recent log |
| `tail -f f` | Follow file live | **Watching logs while reproducing a bug** |
| `wc -l f` | Count lines | "How many rows?" |
| `diff a b` | Show differences | Compare configs / versions |

---

## 3. Identify & inspect files

`file` reads the **magic bytes**, not the extension. Trust it over the filename.

| Command | Does | Use when |
| --- | --- | --- |
| `file f` / `file ./*` | Real type of file(s) | Unknown/renamed file, odd download |
| `strings f` | Readable text inside a binary | Hunting config/URLs in a binary |
| `xxd f` / `xxd -r hex out` | Hex view / reverse hex to binary | Inspecting raw bytes, undoing hex dumps |
| `base64 f` / `base64 -d f` | Encode / decode | JWTs, API tokens, secrets in k8s/Docker |
| `readlink -f f` | Resolve symlink | "Where does this actually point?" |

**What `file` output means → how to open it:**

| `file` says | It is | Open with |
| --- | --- | --- |
| `ASCII text` / `UTF-8 text` | Logs, `.env`, JSON, YAML, SQL | `cat`, `less`, `grep` |
| `data` | Unknown blob | `xxd`, `strings` |
| `gzip compressed data` | `.gz` | `gzip -d`, `zcat` |
| `bzip2 compressed data` | `.bz2` | `bzip2 -d` |
| `POSIX tar archive` | `.tar` | `tar -xf` |
| `Zip archive data` | `.zip` | `unzip` |
| `ELF 64-bit executable` | Linux binary | Run it / `strings` |
| `OpenSSH private key` | `id_rsa`, `id_ed25519` | `ssh -i` (needs `chmod 600`) |
| `symbolic link to X` | Symlink | `readlink -f` |

---

## 4. Find files

```bash
find . -name "*.log"                    # by name (quote the glob)
find . -iname "*.env*"                  # case-insensitive
find . -type f -size +100M              # big files (c=bytes, k, M, G; + bigger, - smaller)
find . -type f -not -executable         # not executable
find . -mtime -1                        # changed in the last day
find / -user bandit7 -group bandit6 2>/dev/null   # by owner/group; hide permission noise
find . -name "*.tmp" -delete            # act on matches (check without -delete first!)
find . -name "*.log" -exec gzip {} +    # run a command on each match
```

Filters: `-type f|d` · `-name` · `-size` · `-user` · `-group` · `-perm 644` · `-mtime`.
**Use when:** you know *something* about the file (name, size, owner, age) but not where it is. Searching `/` needs `2>/dev/null`.

---

## 5. Search and reshape text

### Search: `grep`

```bash
grep "text" f              # matching lines
grep -rn "DATABASE_URL" .  # recursive + filename:line  (find where a setting lives)
grep -i err app.log        # ignore case
grep -v DEBUG app.log      # exclude matches
grep -E "error|fatal" f    # regex OR
grep -C 3 exception f      # 3 lines of context around hit
grep -c ERROR f            # just count matches
```

### Reshape: the log-analysis toolkit

| Command | Does | Example |
| --- | --- | --- |
| `sort` (`-n` numeric, `-r` reverse, `-h` human sizes) | Order lines | `du -sh * \| sort -h` |
| `uniq` (needs sorted input) `-c` count, `-u` only-once | Dedupe / count | `sort f \| uniq -c \| sort -rn \| head` |
| `cut -d',' -f2` | Pick a delimited column | `cut -d, -f2 data.csv` |
| `awk '{print $1}'` | Pick/compute on fields | `awk -F: '{print $1}' /etc/passwd` |
| `tr 'a-z' 'A-Z'` / `tr -d '\r'` | Swap/delete chars (stdin only) | Strip Windows `\r`; ROT13: `tr 'A-Za-z' 'N-ZA-Mn-za-m'` |
| `sed 's/old/new/g' f` | Find/replace | `sed -i` edits in place (macOS: `sed -i ''`) |
| `xargs` | Turn lines into arguments | `grep -l foo * \| xargs rm` |
| `tee f` | Write to file *and* screen | `cmd \| tee out.log` |

### JSON: `jq` (install it)

```bash
curl -s url | jq .                       # pretty-print
curl -s url | jq '.items[].name'         # extract fields
docker inspect ctr | jq '.[0].Mounts'
```

### Edit: `nano f` (easy: `Ctrl+O` save, `Ctrl+X` exit) · `vim f` (`i` insert, `Esc`, `:wq` save+quit, `:q!` abort)

---

## 6. Archives & compression

| Extension | Create | Extract |
| --- | --- | --- |
| `.tar` | `tar -cf a.tar dir/` | `tar -xf a.tar` |
| `.tar.gz` / `.tgz` | `tar -czf a.tar.gz dir/` | `tar -xzf a.tar.gz` (`-C /dest` to pick folder) |
| `.tar.bz2` | `tar -cjf a.tar.bz2 dir/` | `tar -xjf a.tar.bz2` |
| `.gz` (single file) | `gzip f` | `gzip -d f.gz` |
| `.bz2` (single file) | `bzip2 f` | `bzip2 -d f.bz2` |
| `.zip` | `zip -r a.zip dir/` | `unzip a.zip` |

`tar -tzf a.tar.gz` lists contents without extracting. **Use when:** backups, shipping a folder, unpacking downloads/DB dumps.

**Mystery layered file (peel loop):** `file f` → rename to the right extension → decompress → repeat until `ASCII text`. `gzip -d` needs a `.gz` name; `tar -xf` leaves the old archive and creates a *new* file, so `ls` to spot it.

---

## 7. Permissions and users

```
-rwxr-xr--   r=4 w=2 x=1   →  owner / group / others  (rwx=7, r-x=5, r--=4)
```

| Command | Does | Use when |
| --- | --- | --- |
| `chmod 600 f` | Owner read/write only | **SSH private keys, `.env`** (ssh rejects looser keys) |
| `chmod 644 f` / `755 f` | Normal file / script or dir | Default sensible modes |
| `chmod +x script.sh` | Make executable | "Permission denied" running a script |
| `chown user:group f` (`-R` for trees) | Change owner | **Docker volume "permission denied"** (match the container's UID) |
| `sudo cmd` | Run as root | Needs admin; use sparingly |
| `whoami` / `id` | Who am I / my UID, groups | Debug permission problems |
| `su user` | Switch user | Testing as another account |

Unraid note: appdata is usually owned by `nobody:users` (`99:100`).

---

## 8. Processes & system health

| Command | Does | Use when |
| --- | --- | --- |
| `ps aux \| grep name` | Find a process | "Is it running?" |
| `top` / `htop` | Live CPU/RAM per process | Server feels slow |
| `kill PID` / `kill -9 PID` | Stop politely / force | Hung process |
| `ss -tulpn` | What's listening on which port | **"Port already in use"** |
| `lsof -i :5432` | Which process owns a port/file | Same, plus open files |
| `df -h` | Free space per disk | "No space left on device" |
| `du -sh * \| sort -h` | Size of each item, biggest last | Find what's eating the disk |
| `free -h` | RAM usage | Memory pressure |
| `uptime` | Load average, uptime | Quick health check |
| `journalctl -u svc -f` | Service logs (systemd) | Linux service debugging |
| `dmesg \| tail` | Kernel messages | Disk/hardware/OOM errors (Unraid: `/var/log/syslog`) |

Handy: `cmd &` run in background · `jobs` · `nohup cmd &` survives logout · `history | grep x`.

---

## 9. Network

```bash
curl -s url                              # GET
curl -i url                              # include response headers
curl -X POST -H "Content-Type: application/json" -d '{"a":1}' url
curl -O url                              # download keeping filename
curl -H "Authorization: Bearer TOKEN" url
wget url                                 # simple download
ping host                                # is it reachable
dig example.com                          # DNS lookup  (dig example.com MX / @8.8.8.8)
nc -zv host 5432                         # is a TCP port open?
nc host port                             # raw TCP connection (type input by hand)
openssl s_client -connect host:443       # TLS connection (nc can't do TLS)
ip a                                     # my IP addresses
```

**Use when:** testing an API, checking if a service/port is reachable, debugging DNS, confirming a TLS cert.

---

## 10. Remote access (SSH)

```bash
ssh user@host                            # log in
ssh user@host -p 2220                    # non-default port
ssh -i ~/.ssh/id_ed25519 user@host       # log in with a key (key must be chmod 600)
ssh user@host 'df -h'                    # run one command remotely
ssh-keygen -t ed25519                    # create a key pair (.pub = shareable)
ssh-copy-id user@host                    # install your public key (passwordless login)
scp file user@host:/path/                # copy to remote (swap args to pull)
rsync -avh --progress src/ user@host:dst/    # smarter copy: resumes, skips unchanged
```

Server-side keys live in `~/.ssh/authorized_keys`. Shortcut hosts in `~/.ssh/config`:

```
Host unraid
  HostName 192.168.1.10
  User root
  IdentityFile ~/.ssh/id_ed25519
```

then just `ssh unraid`.

---

## 11. Docker

```bash
docker ps -a                       # containers (running + stopped)
docker logs -f --tail 100 ctr      # follow logs          ← first thing when a container misbehaves
docker exec -it ctr sh             # shell inside container (bash if available)
docker inspect ctr | jq            # env, mounts, networks, IP
docker stats                       # live CPU/RAM per container
docker restart|stop|start ctr
docker images                      # local images
docker pull image:tag
docker rm ctr ; docker rmi image   # remove container / image
docker system prune                # clean unused stuff (read the prompt!)
docker compose up -d               # start stack in background
docker compose down                # stop + remove stack
docker compose logs -f svc
docker compose pull && docker compose up -d   # update images
```

**Volume permission errors:** `docker inspect` → find the mount → `ls -ln` the host path → `chown` to the container's UID.

---

## 12. PostgreSQL

```bash
psql -h host -U user -d db                # connect
psql -c "SELECT now();"                   # one-off query
pg_dump -U user db > db.sql               # backup (plain SQL text file)
pg_dump -U user -Fc db > db.dump          # compressed custom format
psql -U user db < db.sql                  # restore from .sql
pg_restore -U user -d db db.dump          # restore from .dump
docker exec -it pg psql -U user db        # psql inside a Postgres container
```

Inside `psql`: `\l` databases · `\c db` switch · `\dt` tables · `\d table` columns · `\x` expanded output · `\q` quit.

---

## 13. Sessions & scheduling

```bash
tmux new -s main                  # new session   (detach: Ctrl+B then D)
tmux attach -t main               # reattach after SSH drops
tmux ls
crontab -e                        # edit scheduled jobs
crontab -l                        # list them
```

Cron format: `min hour day-of-month month day-of-week command` → `0 3 * * * /scripts/backup.sh` = daily at 03:00. Use absolute paths; redirect output (`>> /var/log/job.log 2>&1`).

---

## Recipes

```bash
# Top 10 IPs hitting a web server
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head

# Errors in the last 1000 log lines
tail -n 1000 app.log | grep -i error

# What's eating my disk?
du -sh * | sort -h | tail

# Where is this setting defined?
grep -rn "DATABASE_URL" . --include="*.env*" --include="*.yml"

# Who is using port 8080?
ss -tulpn | grep 8080

# Backup a folder with a dated name
tar -czf backup-$(date +%F).tar.gz /path/to/dir

# Back up the DB nightly (cron: 0 2 * * *)
pg_dump -U user db | gzip > /backups/db-$(date +%F).sql.gz
```

## Safety rules

1. `rm -rf`, `find -delete`, `chmod -R`, `chown -R`: **run the target through `ls`/`find` first.**
2. Never `chmod 777` to "fix" something; find the real owner/permission mismatch.
3. Don't paste secrets into commands (they land in shell history). Use env files or prompts.
4. `docker system prune` and `docker compose down -v` can delete data volumes.
