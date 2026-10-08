# OverTheWire Bandit — Notes

Command reference built up while working through the Bandit levels, grouped by what the commands do. The level where each one first becomes useful is noted in brackets.

## Contents

1. [Navigating and reading files](#1-navigating-and-reading-files)
2. [Finding files](#2-finding-files)
3. [Redirection and `2>/dev/null`](#3-redirection-and-2devnull)
4. [Searching and processing text](#4-searching-and-processing-text)
5. [Binary inspection and encoding](#5-binary-inspection-and-encoding)
6. [Archives and compression](#6-archives-and-compression)
7. [Level 12 walkthrough — peeling compression layers](#7-level-12-walkthrough--peeling-compression-layers)

---

## 1. Navigating and reading files

*[Levels 0–4]*

### `ls` — list directory contents

```bash
ls        # List non-hidden files and directories
ls -l     # Long format: permissions, owner, size, modification date
ls -a     # Include hidden files (names starting with .)
ls -la    # Long format + hidden files (most common usage)
ls -lh    # Human-readable sizes (1K, 234M, 2G)
```

### `cd` — change directory

```bash
cd /path/to/folder   # Go to a specific path
cd ..                # Up one level (parent directory)
cd ../..             # Up two levels
cd ~                 # Home directory
cd -                 # Back to the previous working directory
```

### `cat` — print file contents

```bash
cat filename.txt           # Print the whole file to stdout
cat file1.txt file2.txt    # Print several files one after another
cat -n filename.txt        # Print with line numbers
```

### `file` — identify the real file type

```bash
file filename    # Reads the magic bytes and reports the actual format
```

Example outputs: `ASCII text`, `data`, `gzip compressed data`, `ELF 64-bit executable`.

### `du` — disk usage

```bash
du -h            # Space used by the current directory and subdirectories
du -sh *         # One summary line (-s) per item in the current directory
du -sh /var/log  # Total size of a specific directory
```

---

## 2. Finding files

*[Levels 5–6]*

### `find` — search a directory tree

```bash
find . -name "file.txt"           # By name, in the current directory and below
find . -type f -size 1033c        # Regular files of exactly 1033 bytes
find /var -user bandit1           # Files under /var owned by user bandit1
find . -type f -not -executable   # Regular files that are NOT executable
```

### Common filters

| Filter | Meaning |
| --- | --- |
| `.` or `/` | Where to start: current directory, or the whole filesystem from root |
| `-name "x"` | File name matches `x` |
| `-type f` | Regular files only |
| `-size 33c` | Exactly 33 bytes (`c` = bytes) |
| `-user bandit7` | Owned by user `bandit7` |
| `-group bandit6` | Owned by group `bandit6` |
| `-not -executable` | Not executable |

### Level 6 solution

Find a file anywhere on the server that is owned by user `bandit7`, group `bandit6`, and is 33 bytes:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Searching from `/` hits many directories you cannot read, so `2>/dev/null` hides the "Permission denied" messages and leaves only the matching path (explained in the next section).

---

## 3. Redirection and `2>/dev/null`

*[Level 6]*

Linux gives every process three numbered data streams (file descriptors):

| Number | Name | What it carries |
| --- | --- | --- |
| `0` | `stdin` | Input (keyboard) |
| `1` | `stdout` | Normal command output |
| `2` | `stderr` | Error messages |

Breaking down `2>/dev/null`:

- **`2`** — the stream to redirect: `stderr`.
- **`>`** — the redirection operator: send the stream on the left to the location on the right.
- **`/dev/null`** — the null device, a special file that discards everything written to it (a black hole).

Result: errors are thrown away, normal output still prints.

---

## 4. Searching and processing text

*[Levels 7–11]*

### `grep` — search text for a pattern

```bash
grep "pattern" file.txt      # Lines containing the pattern
grep -i "pattern" file.txt   # Case-insensitive
grep -rn "pattern" .         # Recursive, with line numbers
```

### `sort` — order lines

```bash
sort file.txt      # Alphabetical
sort -n file.txt   # Numerical
sort -r file.txt   # Reversed
```

### `uniq` — filter repeated lines

`uniq` only compares **adjacent** lines, so always `sort` first.

```bash
sort file.txt | uniq      # Remove duplicates
sort file.txt | uniq -u   # Only lines that appear exactly once
sort file.txt | uniq -c   # Count occurrences of each line
```

### `tr` — translate or delete characters

`tr` reads from standard input only, so pipe the file into it.

```bash
cat file.txt | tr 'a-z' 'A-Z'                 # Convert to uppercase
cat file.txt | tr -d '\r'                     # Delete specific characters
cat file.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'     # Decode ROT13
```

---

## 5. Binary inspection and encoding

*[Levels 9–12]*

### `strings` — pull readable text out of a binary

```bash
strings file.bin        # Print the ASCII strings found inside
strings -n 8 file.bin   # Only strings at least 8 characters long
```

### `base64` — encode / decode Base64

```bash
base64 file.txt          # Encode
base64 -d encoded.txt    # Decode back to raw data
```

### `xxd` — hex dumps

```bash
xxd file.bin                     # View hex + ASCII representation
xxd -r hex.txt > output.bin      # Reverse a hex dump back to binary
```

---

## 6. Archives and compression

*[Level 12]*

| Tool | Extension | Purpose |
| --- | --- | --- |
| `tar` | `.tar` | Bundles many files into one archive (no compression by itself) |
| `gzip` | `.gz` | Standard LZ77 compression |
| `bzip2` | `.bz2` | Higher-ratio compression |

### `tar`

```bash
tar -cvf archive.tar dir/      # Create an archive
tar -xvf archive.tar           # Extract an archive
tar -ztvf archive.tar.gz       # List contents of a gzipped archive
```

### `gzip`

```bash
gzip file.txt      # Compress into file.txt.gz
gzip -d file.gz    # Decompress
```

### `bzip2`

```bash
bzip2 file.txt      # Compress into file.txt.bz2
bzip2 -d file.bz2   # Decompress
```

**Tip:** when a file has been compressed several times over, run `file` on it after each step to see which tool to use next.

---

## 7. Level 12 — peeling compression layers

*[Level 12 → 13]*

`data.txt` is a hex dump of a repeatedly compressed file. Work in `cd $(mktemp -d)`, `cp` the file in, run `xxd -r data.txt data`, then loop: **`file` → rename to match → undo** until it says `ASCII text`.

Layers: `hex → gzip → bzip2 → gzip → tar → tar → bzip2 → tar → gzip → text`

| `file` says | Undo with |
| --- | --- |
| `gzip compressed data` | `mv f f.gz && gzip -d f.gz` |
| `bzip2 compressed data` | `bzip2 -d f` (output: `f.out`) |
| `POSIX tar archive` | `tar -xf f` (adds a new file; keep going with that one) |
| `ASCII text` | `cat f` — done |

**Gotchas:** trust `file`, not the extension; `gzip -d` needs a `.gz` name; `tar -xf` keeps the old archive, so `ls` for the new file.
