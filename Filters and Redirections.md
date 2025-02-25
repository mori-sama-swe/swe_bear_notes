Filters and Redirections
#sre/linux


#### Filters In Linux:
Filters are commands that take input, process it, and produce output. They are typically used with pipes (|) to process text streams.

`grep` **- Search for a pattern in a file**
```bash
# Input: file.txt contains:
# Hello World
# Linux is great
# I love Linux

grep "Linux" file.txt
# Output:
# Linux is great
# I love Linux
```

![](Filters%20and%20Redirections/Screenshot%202025-02-01%20at%2010.58.16%E2%80%AFPM.png)
---
`sort` - sort lines alphabetically
```bash
# Input: names.txt contains:
# Charlie
# Alice
# Bob

sort names.txt
# Output:
# Alice
# Bob
# Charlie
```

![](Filters%20and%20Redirections/Screenshot%202025-02-01%20at%2011.00.18%E2%80%AFPM.png)
---
`uniq` - removes duplicate lines
```bash
# Input (sorted): colors.txt contains:
# Red
# Red
# Blue
# Blue
# Green

uniq colors.txt
# Output:
# Red
# Blue
# Green
```
---
`wc` - count lines, words, and characters
```bash
# Input: file.txt contains:
# Hello World
# Linux is awesome

wc file.txt
# Output:
# 2  5  27 file.txt  # (Lines, Words, Characters)
```
---
`cut` -  extract a column from a file
```bash
# Input: users.txt contains:
# Alice:25:Developer
# Bob:30:Manager

cut -d':' -f1 users.txt
# Output:
# Alice
# Bob
```
---
`print` - print specific fields
```bash
# Input: data.txt contains:
# Alice 25 Developer
# Bob 30 Manager

awk '{print $1, $3}' data.txt
# Output:
# Alice Developer
# Bob Manager
```
---
`sed` -  replace text in a file
```bash
# Input: info.txt contains:
# I love Windows

sed 's/Windows/Linux/' info.txt
# Output:
# I love Linux
```
---
#### Redirection In Linx:
Redirection is used to direct input/output to files or other commands.


