Terminal Variables
#sre/data_serialization

### Storing Varaibles In Terminal

To store a variable, use the following syntax:
```bash
VARIABLE_NAME="some_value"
```
---
### Retrieving a Variable

To retrieve the value of a variable, prefix it with a $ and use the echo command:
```bash
echo $VARIABLE_NAME
```
---
### Exporting Variables (Making Them Available to Subshells)

By default, variables set this way are **only available in the current shell session**. If you want to make them available to subshells (e.g., when running scripts), use export:

A **subshell** is a child process started by your current shell session. It inherits variables and settings from the parent shell but runs as a separate instance. When the subshell exits, changes made inside it do not affect the parent shell.

```bash
export VARIABLE_NAME="some_value"
```
- Now, the variable will persist in child processes of the shell.
---
### Listing All Environment Variables
To see all currently set environment variables, use:
```bash
printenv
```
To See a Specific Variable:
```bash
printenv VARIABLE_NAME
```
---
### Unsetting (Removing) a Variable
```bash
unset VARIABLE_NAME
```
---
![](Terminal%20Variables/Screenshot%202025-02-10%20at%2010.23.21%E2%80%AFPM.png)