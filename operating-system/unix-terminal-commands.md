# Basic Unix Terminal Commands

Unix-like operating systems, including Linux, provide a powerful command-line interface (CLI) for managing and interacting with your system. Here are some basic terminal commands:

## Navigation

### `pwd`

- Print the current working directory.

### `ls`

- List the contents of a directory.
- `ls -l`: Detailed list with file permissions.
- `ls -a`: Show hidden files.

### `cd`

- Change directory.
- `cd <directory>`: Navigate to a specific directory.
- `cd ..`: Move up one level.

## File Operations

### `touch`

- Create an empty file.
- `touch <filename>`: Create a file.

### `mkdir`

- Create a new directory.
- `mkdir <directoryname>`: Create a directory.

### `cp`

- Copy files or directories.
- `cp <source> <destination>`: Copy a file or directory.

### `mv`

- Move or rename files or directories.
- `mv <source> <destination>`: Move or rename a file or directory.

### `rm`

- Remove files or directories.
- `rm <filename>`: Remove a file.
- `rm -r <directoryname>`: Remove a directory and its contents.

## Viewing and Editing Files

### `cat`

- View the contents of a file.
- `cat <filename>`: Display the contents of a file.

### `less` and `more`

- View the contents of a file page by page.
- `less <filename>`: Use the arrow keys to navigate.

### `nano` or `vim`

- Text editors for creating and editing files.
- `nano <filename>` or `vim <filename>`: Open a file for editing.

## File Permissions

### `chmod`

- Change file permissions.
- `chmod <permissions> <filename>`: Modify file permissions.

## Searching and Finding

### `find`

- Search for files and directories.
- `find <directory> -name <filename>`: Search for a specific file.

### `grep`

- Search for text within files.
- `grep <pattern> <filename>`: Search for a specific pattern in a file.

## Process Management

### `ps`

- List running processes.

### `top` or `htop`

- Monitor system processes in real-time.

### `kill`

- Terminate processes.
- `kill <processID>`: Terminate a process.

## System and Network

### `lsof`

- List open files and processes.

### `curl`

- Transfer data with URLs.
  - `curl https://example.com`: Make a simple GET request.
  - `curl -O https://example.com/somefile.txt`: Download a file.
  - `curl -d "key1=value1&key2=value2" -X POST https://example.com/api`: Send POST data.
  - `curl -i https://example.com`: View response headers.
  - `curl -H "User-Agent: MyUserAgent" https://example.com`: Add custom headers.

### `wget`

- Download files from the web.

### `tail`

- Display the last few lines of a text file.

### `head`

- Display the first few lines of a text file.

### `dig`

- Query DNS servers for domain information.
  - `dig example.com`: Basic domain query.
  - `dig example.com MX`: Query for specific DNS record type.
  - `dig example.com @8.8.8.8`: Query a specific DNS server.

### `sed`

- **SED** stands for **Stream Editor**.
- Used for text manipulation and substitutions.
- Example: Replace "old" with "new" in a file:
  ```bash
  sed 's/old/new/g' filename.txt
  ```

### `awk`

- **AWK** is a versatile text processing tool.
- Named after its creators: Aho, Weinberger, and Kernighan.
- Useful for data extraction, manipulation, and reporting.
- Example: Calculate the sum of the third column in a file:

  ```bash
  awk '{sum+=$3} END {print sum}' datafile.txt
  ```

These are some of the fundamental Unix terminal commands. To get more information on any of these commands, you can use the `man` command followed by the command name. For example, `man ls` will display the manual page for the `ls` command, explaining its usage and options in detail.

```bash
ssh -i <ssh key> <user>@<ip address>

#

su <user>


```

```bash
cat /etc/passwd
**-/
# See all users
```
