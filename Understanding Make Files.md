Understanding Make Files
#sre/makefile

[Makefile Tutorial by Example](https://makefiletutorial.com/)

why do make files exist?:
- when you need a series of instructions to run depending on what files have changed
- the goal of makefiles is to compile whatever files need to be compiled, based on what files have changed

example:
```makefile
hello:
	echo "Hello World"
```

output:
![](Understanding%20Make%20Files/image.png)

---
### Makefile Syntax:

a makefile consists of a set of rules:
```makefile
targets: prerequisities
	commands
```

* The *targets* are file names, separated by spaces. Typically, there is only one per rule.
* The *commands* are a series of steps typically used to make the target(s). These *need to start with a tab character*, not spaces.
* The *prerequisites* are also file names, separated by spaces. These files need to exist before the commands for the target are run. These are also called *dependencies*
---
Example:
```makefile
hello: 
	echo "this line will print if the file hello does not exist"
```

There's already a lot to take in here. Let's break it down:
* We have one *target* called hello
* This target has two *commands*
* This target has no *prerequisites*

**We'll then run make hello. As long as the hello file does not exist, the commands will run. If hello does exist, no commands will run.**

It's important to realize that I'm talking about hello as both a *target* and a *file*. That's because the two are directly tied together.
- Typically, when a target is run (aka when the commands of a target are run), the commands will create a file with the same name as the target. In this case, the hello *target* does not create the hello *file*.

Example of Hello File Already Created: 
- output: “hello” is up to date 

```makefile
hello: 
	echo "this line will print if the file hello does not exist"
```

![](Understanding%20Make%20Files/image%202.png)

---
Essence of Makefiles:

- it uses the filesystem timestamps as a proxy to determine if something has changed. This is a reasonable heuristic, because file timestamps typically will only change if the files are modified.

---
### Variables In Makefiles

variables can only be strings, and are used via `:=` 
```makefile

name := patrick victoria
file_dont_exist:
	echo "The Following Names: " $(name)
```

![](Understanding%20Make%20Files/Screenshot%202025-01-26%20at%2011.23.35%E2%80%AFPM.png)
