# vscode
#software-engineering/vscode

### C++
You can set up VS Code to build and launch your application without manually running the makefile by adding a tasks and launch configuration. Create two files in your workspace's .vscode folder:

1) **tasks.json** – This file defines a build task that compiles your program.
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build my_program",
            "type": "shell",
            "command": "clang++",
            "args": [
                "-std=c++20",
                "-Wall",
                "-Wextra",
                "-Wpedantic",
                "-O2",
                "main.cpp",
                "-lcurl",
                "-lgumbo",
                "-o",
                "my_program"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

2) **launch.json** – This file defines a debug configuration that runs your program.
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch my_program",
            "type": "lldb-dap",
            "request": "launch",
            "program": "${workspaceFolder}/my_program",
            "args": [],
            "cwd": "${workspaceFolder}",
            "stopOnEntry": false,
            "preLaunchTask": "build my_program",
        }
    ]
}
```