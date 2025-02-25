File Types
#sre/linux

In Linux, file types are categorized based on their functionality and structure. You can check the type of a file using the ls -l command (which displays file type indicators) or the file command.

Everything We Do In Linux Is A File, The Difference Is The Type of Files

check what type of file:
- its good to know -> what type of files it is so we can use the correct commands

```bash
file {filename}
```


#### Types of Files:
**Regular Files:** these include text files, binary files, and executable files
- `.txt` , `.log`
- `.sh`, `.out`
- `.conf`

**Directory:** is a type of fiel that contain other files and subdirectories
ex: `/home/user/Documents/`![](File%20Types/Screenshot%202025-02-01%20at%2010.22.50%E2%80%AFPM.png)

**Symbolic Links:** (soft link) points to another file or directory, acts as a shortcut
```bash
ln -s /path/to/original /path/to/link
```

![](File%20Types/Screenshot%202025-02-01%20at%2010.38.06%E2%80%AFPM.png)

