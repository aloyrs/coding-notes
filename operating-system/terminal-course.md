# Terminal Course: Guided Walkthrough

Hands-on lessons that go with [[terminal-cheatsheet]]. Do them in order; each builds on the last. Tick the box when you've done the exercise.

**Setup:** practise in a scratch folder so nothing real gets hurt.

```bash
cd $(mktemp -d) && pwd
```

**Priority:** lessons 1, 3, 5, 6, 7, 10, 12, 13 cover most daily use. The rest are lookups: read once, return when you hit the problem.

---

## Module 1: Foundations (Cheatsheet §0-2)

### Lesson 1: Pipes and redirects (§0)
The most important idea. Every command prints text; `|` feeds that text into the next command.
- `|` chain · `>` save to file · `2>/dev/null` hide errors · `&&` run next only if this worked
- [ ] `ls -la | grep ".zsh"`, then `ls -la > files.txt`

### Lesson 2: Moving around (§1)
`pwd`, `ls -lah`, `cd`, `mkdir -p`, `cp`, `mv`, `rm`.
- `mv` also renames. `rm` has no trash: `ls` the target before deleting.
- [ ] Make `a/b/c`, `touch` a file in it, copy it, rename the copy, delete the folder

### Lesson 3: Reading files (§2)
Pick the tool by file size: small → `cat`, big → `less`, ends → `head`/`tail`.
- `tail -f` follows a log live. You'll use it every time you debug.
- [ ] `tail -n 20 /etc/hosts`, then `less /etc/passwd` (`/root` to search, `q` to quit)

---

## Module 2: Finding things (§3-5)

### Lesson 4: What is this file? (§3)
Never trust the extension; run `file` first. Use the table to map output to a tool: gzip → `gzip -d`, tar → `tar -xf`, SSH key → `chmod 600`. `base64 -d` decodes JWTs and API tokens.
- [ ] `file /bin/ls ~/.zshrc`, then `echo 'aGVsbG8=' | base64 -d`

### Lesson 5: `find` (§4)
Use when you know something about a file (name, size, age, owner) but not where it is.
- Combine `-name`, `-size`, `-mtime`, `-user`, `-type f`.
- Add `2>/dev/null` when searching from `/`. Test without `-delete` before adding it.
- [ ] `find ~ -type f -size +50M 2>/dev/null` (your biggest files)

### Lesson 6: `grep` (§5)
Use when you know the text but not the file.
- Core flags: `-r` recursive · `-n` line numbers · `-i` ignore case · `-v` invert · `-C 3` context
- [ ] `grep -rn "localhost" ~/docs/coding-notes | head`

### Lesson 7: The text toolkit (§5)
Combine small tools into pipelines. The "top N of anything" pattern:

```
extract column → sort → uniq -c → sort -rn → head
```

`uniq` only sees adjacent lines, so `sort` first. `awk` = columns, `sed` = find/replace, `jq` = JSON, `xargs` = results as arguments.
- [ ] `awk -F: '{print $NF}' /etc/passwd | sort | uniq -c | sort -rn` (users per login shell)

---

## Module 3: Housekeeping (§6-8)

### Lesson 8: Archives (§6)
Memorise two commands; the rest of the table is lookup:

```bash
tar -czf x.tar.gz dir/    # pack
tar -xzf x.tar.gz         # unpack   (-tzf lists contents safely first)
```

- [ ] Pack a folder with a dated name (`$(date +%F)`), list it, extract it elsewhere with `-C`

### Lesson 9: Permissions (§7)
Read `-rwxr-xr--` as owner / group / others, where r=4, w=2, x=1.
- `chmod 600` keys and `.env` · `chmod +x` scripts · `chown` for Docker volume errors · never `chmod 777`
- [ ] `ls -l ~/.zshrc`, then work out its number from the letters

### Lesson 10: Health checks (§8)
Ask a question, use the matching command:

| Question | Command |
| --- | --- |
| Is it running? | `ps aux \| grep x` |
| Is it slow? | `top` / `htop` |
| Disk full? | `df -h`, then `du -sh * \| sort -h` |
| Port taken? | `ss -tulpn` |
| What holds the port? | `lsof -i :PORT` |

- [ ] `df -h`, then `du -sh ~/* | sort -h | tail`

---

## Module 4: Servers and your stack (§9-13)

### Lesson 11: Network (§9)
`curl` is the one to master: `-i` headers · `-X POST -d` send data · `-H` add header. `nc -zv host port` tests a port, `dig` is DNS, `openssl s_client` is TLS.
- [ ] `curl -i https://example.com`, then `nc -zv example.com 443`

### Lesson 12: SSH (§10)
`ssh user@host` → keys (`ssh-keygen -t ed25519`, `ssh-copy-id`) → a `Host unraid` block in `~/.ssh/config` so you can type `ssh unraid`. `scp` copies once; `rsync -avh` is better for folders and re-runs.
- [ ] Set up the config block for your Unraid box and log in with a key

### Lesson 13: Docker (§11)
Debug order when a container misbehaves:

1. `docker ps -a`
2. `docker logs -f --tail 100 ctr`
3. `docker exec -it ctr sh`
4. `docker inspect ctr | jq` if still unclear

Volume permission error: inspect the mount → `ls -ln` the host path → `chown` to the container's UID. Careful with `docker system prune` and `compose down -v`.
- [ ] Walk through the 4 steps on one of your running containers

### Lesson 14: Postgres (§12)
Connect `psql`, back up `pg_dump db > file.sql`, restore `psql db < file.sql`. In `psql`: `\dt` tables, `\q` quit.
- [ ] Back up a local DB, restore it into a new empty one

### Lesson 15: Sessions and scheduling (§13)
- `tmux` keeps work alive when SSH drops: detach `Ctrl+B` then `D`, reattach `tmux attach`.
- `crontab -e` schedules jobs: `0 3 * * *` = daily 03:00. Use absolute paths and redirect output to a log.
- [ ] Start a tmux session, detach, reattach

---

## Capstone

Run the Recipes at the bottom of the cheatsheet on your real server. Best one: a nightly cron job running `pg_dump | gzip` into a dated file. It uses pipes, redirects, `date`, cron, Postgres and permissions together.

- [ ] Nightly DB backup cron job running and verified (restore tested once)
