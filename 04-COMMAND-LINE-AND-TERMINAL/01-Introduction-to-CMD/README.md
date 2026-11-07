
# 01 — Introduction to Windows Command Prompt (CMD)

## 1. What is CMD?

CMD stands for **Command Prompt**. It is a command-line interpreter available in Microsoft Windows.

It allows users to interact with the operating system by entering text-based commands instead of using graphical elements such as buttons, menus, and icons.

CMD executes commands to perform operations such as:
- Managing files and directories.
- Viewing system information.
- Managing processes.
- Configuring network settings.
- Running programs.
- Automating repetitive tasks.

CMD is also commonly known as Windows Command Processor.

Its executable file is:

```text
cmd.exe
```

---

## 2. What is a Command-Line Interface (CLI)?

A Command-Line Interface (CLI) is a text-based interface through which users communicate with a computer by entering commands.

Instead of clicking graphical elements, users type instructions that are interpreted and executed by a command-line program.

### Example

Creating a folder:

Using GUI:
1. Open File Explorer.
2. Navigate to a location.
3. Right-click.
4. Select New → Folder.
5. Enter a folder name.

Using CMD:

```cmd
mkdir MyFolder
```

Both methods achieve the same result.

### Advantages of CLI

- Faster execution of repetitive operations.
- Supports automation.
- Requires fewer graphical resources.
- Allows precise system administration.
- Makes scripting possible.
- Useful for remote system management.

### Disadvantages of CLI

- Requires knowledge of commands.
- Incorrect commands may modify or delete data.
- Some operations are difficult to understand initially.
- Does not provide the same visual experience as GUI applications.

---

## 3. CLI vs GUI

| Feature | CLI | GUI |
|---|---|---|
| Full Form | Command-Line Interface | Graphical User Interface |
| Interaction | Text commands | Visual elements |
| Input | Keyboard | Mouse and keyboard |
| Learning | Requires command knowledge | Generally easier |
| Automation | Highly suitable | Often more limited |
| Resource Usage | Generally lower | Generally higher |
| Examples | CMD, Bash | File Explorer, Windows Settings |

---

## 4. What is a Shell?

A shell is a program that provides an interface between the user and the operating system.

It accepts commands, interprets them, and requests the operating system to perform the required operations.

Examples of command interpreters and shells:

| Shell | Platform |
|---|---|
| CMD | Windows |
| PowerShell | Windows, Linux, macOS |
| Bash | Linux, macOS and other Unix-like systems |
| Zsh | Linux, macOS and other Unix-like systems |

### How a Shell Works

1. The user enters a command.
2. The shell reads the command.
3. The shell interprets its syntax and arguments.
4. The requested command or program is executed.
5. The result is displayed to the user.

---

## 5. What is a Terminal?

A terminal is an application that provides a text-based interface for interacting with a shell.

Historically, terminals were physical devices connected to computers.

Modern operating systems use terminal emulators.

Examples:

- Windows Terminal
- GNOME Terminal
- macOS Terminal
- Konsole

### Terminal vs Shell

| Terminal | Shell |
|---|---|
| Provides the interface | Interprets commands |
| Displays input and output | Executes command logic |
| Hosts a shell | Runs inside a terminal in typical desktop usage |
| Example: Windows Terminal | Example: PowerShell |

**Important:** Windows Terminal is not the same thing as CMD. Windows Terminal can host CMD, PowerShell and other shells.

---

## 6. CMD vs PowerShell vs Windows Terminal

| Feature | CMD | PowerShell | Windows Terminal |
|---|---|---|---|
| Type | Command interpreter | Shell and scripting environment | Terminal emulator |
| Primary Use | Traditional Windows commands | Automation and administration | Hosting command-line environments |
| Scripting | Batch scripting | PowerShell scripting | No independent shell language |
| Output | Primarily text | Structured .NET objects | Displays hosted application output |
| Executable | cmd.exe | pwsh.exe / powershell.exe | WindowsTerminal.exe |

### CMD

CMD is the traditional Windows command interpreter.

Example:

```cmd
dir
```

### PowerShell

PowerShell is a modern command-line shell and scripting environment.

Example:

```powershell
Get-ChildItem
```

### Windows Terminal

Windows Terminal is a modern terminal application that can host different command-line environments.

---

## 7. History of CMD

CMD evolved from Microsoft's earlier command-line environments.

Important milestones:

- MS-DOS: Introduced the command-line environment used by early Microsoft operating systems.
- Windows NT: Introduced the Windows NT command interpreter, commonly known as CMD.
- Windows XP: Continued CMD support as part of the Windows NT family.
- Windows 10: CMD remained available alongside PowerShell and Windows Terminal.
- Windows 11: CMD continues to be supported, including through Windows Terminal.

CMD remains useful for Windows compatibility, batch scripts, system troubleshooting and command-line operations.

---

## 8. Understanding the CMD Interface

When CMD opens, you may see something similar to:

```cmd
C:\Users\YourName>
```

Let's understand each component.

| Component | Meaning |
|---|---|
| C: | Current drive |
| \ | Directory separator |
| Users | Directory |
| YourName | Current user's directory |
| > | Command prompt symbol |

The complete path indicates the current working directory.

### Example

```cmd
C:\Users\Varun>
```

This means the current working directory is:

```text
C:\Users\Varun
```

The actual username and directory may differ on your computer.

---

## 9. How to Open CMD

### Method 1: Run Dialog

1. Press `Win + R`.
2. Type `cmd`.
3. Press Enter.

### Method 2: Start Menu

1. Open the Start Menu.
2. Search for Command Prompt.
3. Select the application.

### Method 3: Windows Terminal

1. Open Windows Terminal.
2. Open the profile dropdown.
3. Select Command Prompt.

### Administrator Mode

Some commands require elevated privileges.

To open CMD as administrator:

1. Search for Command Prompt.
2. Right-click the application.
3. Select Run as administrator.
4. Approve the User Account Control prompt.

**Warning:** Administrator mode gives commands greater system access. Use it only when necessary.

---

## 10. Understanding Command Structure

A typical CMD command contains:

```text
command [options] [arguments]
```

Components:

- Command: The operation to perform.
- Options: Modify how the command behaves.
- Arguments: Values or targets supplied to the command.

### Example

```cmd
dir /s C:\Users
```

Explanation:

- `dir`: Command to list directory contents.
- `/s`: Option to include subdirectories.
- `C:\Users`: Target directory.

Not every command requires options or arguments.

---

## 11. Types of CMD Commands

CMD commands can broadly be classified into two categories.

### A. Internal Commands

Internal commands are implemented by the command interpreter itself.

They do not require a separate executable file for the command.

Examples:

```cmd
cd
dir
cls
copy
del
echo
mkdir
rmdir
ren
type
```

These commands are handled by `cmd.exe`.

### B. External Commands

External commands are provided by separate executable programs.

Examples:

```cmd
ipconfig
ping
tracert
tasklist
systeminfo
chkdsk
```

Their executable files are generally located in Windows system directories or other directories listed in PATH.

---

## 12. Important Concepts in CMD

### Current Working Directory

The directory in which CMD currently operates.

Example:

```cmd
C:\Users\Varun>
```

### Absolute Path

A complete path beginning from a drive root or another filesystem root.

Example:

```text
C:\Users\Varun\Documents\Notes.txt
```

### Relative Path

A path interpreted relative to the current working directory.

Example:

```text
Documents\Notes.txt
```

### Command Interpreter

The program responsible for interpreting command-line instructions.

In Windows CMD:

```text
cmd.exe
```

### Executable File

A file that contains a program that can be executed by the operating system.

Common Windows executable extensions include:

- `.exe`
- `.com`
- `.bat`
- `.cmd`

---

## 13. How CMD Executes Commands

A simplified execution process:

```text
User
  |
  v
Enters Command
  |
  v
CMD Interpreter (cmd.exe)
  |
  v
Command Parsing
  |
  v
Command Identification
  |
  +------ Internal Command
  |
  +------ External Program
  |
  v
Windows Operating System
  |
  v
Execution Result
  |
  v
Output in CMD
```

The exact execution process varies depending on the command.

For external programs, CMD locates the executable using the supplied path or executable search rules, including PATH.

---

## 14. Applications and Uses of CMD

CMD is commonly used for:

### File Management
- Creating directories.
- Copying files.
- Moving files.
- Renaming files.
- Deleting files.

### System Administration
- Inspecting system information.
- Managing processes.
- Checking disks.
- Running administrative utilities.

### Networking
- Checking IP configuration.
- Testing connectivity.
- Inspecting network routes.
- Troubleshooting DNS.

### Software Development
- Running programs.
- Executing scripts.
- Managing development workflows.
- Starting local servers.
- Working with Git and other command-line tools.

### Automation
- Creating batch scripts.
- Automating repetitive operations.
- Combining multiple commands.
- Scheduling scripts.

---

## 15. Limitations of CMD

Despite its usefulness, CMD has limitations:

1. Limited scripting capabilities compared with PowerShell.
2. Primarily text-oriented command processing.
3. Less convenient for complex system administration.
4. Limited native support for structured objects.
5. Older command syntax and conventions.
6. Some modern administrative tasks are better handled using PowerShell.

---

## 16. Important CMD Terms — Quick Reference

| Term | Definition |
|---|---|
| CMD | Windows Command Prompt |
| CLI | Command-Line Interface |
| GUI | Graphical User Interface |
| Shell | Command interpreter |
| Terminal | Application providing access to a shell |
| cmd.exe | Windows Command Processor executable |
| Command | Instruction entered into a shell |
| Argument | Value passed to a command |
| Option | Modifier that changes command behavior |
| Path | Location of a file or directory |
| Working Directory | Current operating directory |
| Executable | Program file that can be run |
| PATH | Environment variable containing executable search directories |
| Batch File | Script containing Windows command-line instructions |

---

## 17. Key Takeaways

- CMD is the traditional command interpreter in Windows.
- CLI allows users to interact with computers using text commands.
- A shell interprets commands and coordinates their execution.
- A terminal provides the interface in which a shell runs.
- CMD supports internal and external commands.
- CMD can manage files, directories, processes, networks and system operations.
- Batch scripting allows repetitive tasks to be automated.
- PowerShell provides more advanced scripting and administration capabilities.

---

## 18. Further Learning

Official Microsoft documentation:

- [Windows Commands](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [Command Prompt Documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmd)
- [Windows Terminal Documentation](https://learn.microsoft.com/en-us/windows/terminal/)
- [PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)

---

**END OF LESSON 01 — INTRODUCTION TO WINDOWS COMMAND PROMPT**
