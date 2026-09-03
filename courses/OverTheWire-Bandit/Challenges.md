# Level 0

```bash

# connect remotely with username , hostname and port , will be prompted by password 
ssh bandit0@bandit.labs.overthewire.org -p 2220

#password
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

```bash
# --- 1. ls (List Directory Contents) ---
ls                    # List non-hidden files and directories
ls -l                 # Long listing format (permissions, owner, size, modification date)
ls -a                 # List all files, including hidden files (starting with .)
ls -la                # Combine long listing + all files (most common usage)
ls -lh                # Human-readable sizes (e.g., 1K, 234M, 2G)


# --- 2. cd (Change Directory) ---
cd /path/to/folder    # Navigate to a specific directory path
cd ..                 # Move up one level (parent directory)
cd ../..              # Move up two levels
cd ~                  # Navigate to your user's home directory
cd -                  # Switch back to the previous working directory


# --- 3. cat (Concatenate & Print File Contents) ---
cat filename.txt      # Display the entire raw text of a file to stdout
cat file1.txt file2.txt # Display multiple files concatenated together
cat -n filename.txt   # Display file content with line numbers


# --- 4. file (Determine File Type) ---
file filename         # Inspect magic bytes to report the real file format
                      # Output example: ASCII text, Data, Gzip compressed, ELF 64-bit executable


# --- 5. du (Disk Usage) ---
du -h                 # Display disk space used by current directory and subdirectories (human-readable)
du -sh *              # Summary (-s) of size for each item in current directory
du -sh /var/log       # Check total size of a specific directory


# --- 6. find (Search Directory Tree) ---
find . -name "file.txt"          # Find files named "file.txt" in current directory (.) and subfolders
find . -type f -size 1033c       # Find regular files (-type f) of exact size 1033 bytes (c)
find /var -user bandit1          # Search /var for files owned by user "bandit1"
find . -type f -not -executable  # Find files that are regular files and NOT executable
```

# Level 1

```bash
# for special char like '-' 
cat ./-

# Password 
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

