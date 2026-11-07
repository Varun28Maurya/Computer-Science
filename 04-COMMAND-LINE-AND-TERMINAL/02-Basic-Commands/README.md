
# 02 — CMD Basic Commands

## 1. Introduction

CMD provides several built-in commands that allow users to interact with Windows.

Basic commands are used to:
- Display information.
- Clear the terminal.
- Print messages.
- Check system details.
- Navigate the command environment.
- Access command documentation.
- Control the CMD session.

Understanding these commands is essential before learning file management, networking and scripting.

---

## 2. HELP — Display Available Commands

### Purpose

The `help` command displays a list of available Windows commands.

### Syntax

```cmd
help
```

### Example

```cmd
help
```

### Expected Output

Displays a list of commands supported by CMD, along with brief descriptions.

### Additional Usage

To get help for a particular command:

```cmd
help dir
help copy
help mkdir
```

Another way to access command documentation is:

```cmd
dir /?
copy /?
ipconfig /?
```

The `/?` option displays help for the specified command.

---

## 3. CLS — Clear the Screen

### Purpose

The `cls` command clears the CMD screen.

### Syntax

```cmd
cls
```

### Example

```cmd
cls
```

### Explanation

It removes previously displayed text from the visible terminal window.

It does not delete files, command history or system information.

---

## 4. VER — Display Windows Version

### Purpose

The `ver` command displays the Windows version information reported by the command interpreter.

### Syntax

```cmd
ver
```

### Example

```cmd
ver
```

### Expected Output

```text
Microsoft Windows [Version 10.0.xxxxx.xxxx]
```

The actual version number depends on your Windows installation.

### Use Cases

- Checking the Windows version.
- Basic operating system identification.
- Troubleshooting compatibility issues.

Note: `ver` does not provide the complete Windows edition and build details.

---

## 5. WHOAMI — Display Current User

### Purpose

The `whoami` command displays the account identity associated with the current command session.

### Syntax

```cmd
whoami
```

### Example

```cmd
whoami
```

### Expected Output

```text
computer-name\username
```

### Additional Options

Display the user's groups:

```cmd
whoami /groups
```

Display user privileges:

```cmd
whoami /priv
```

Display the user's security identifier:

```cmd
whoami /user
```

### Use Cases

- Checking the current account.
- Understanding user permissions.
- Troubleshooting access issues.
- Identifying group memberships.

---

## 6. HOSTNAME — Display Computer Name

### Purpose

The `hostname` command displays the name assigned to the computer.

### Syntax

```cmd
hostname
```

### Example

```cmd
hostname
```

### Expected Output

```text
DESKTOP-ABC123
```

The output depends on your computer's configured hostname.

### Use Cases

- Identifying a computer on a network.
- Troubleshooting network connections.
- Checking the machine name before remote administration.

---

## 7. ECHO — Display Text

### Purpose

The `echo` command displays text or variable values in CMD.

### Syntax

```cmd
echo [message]
```

### Examples

Display a message:

```cmd
echo Hello World
```

Display your current directory:

```cmd
echo %CD%
```

Display the username variable:

```cmd
echo %USERNAME%
```

Display the computer name:

```cmd
echo %COMPUTERNAME%
```

### Turn Command Echoing Off

```cmd
echo off
```

This prevents CMD from displaying subsequently executed commands in a batch script.

### Turn Command Echoing On

```cmd
echo on
```

### Display Whether Echo Is Enabled

```cmd
echo
```

### Important Note

The `@echo off` combination is commonly used at the beginning of batch files.

```cmd
@echo off
echo Welcome to CMD
```

---

## 8. DATE — Display or Change Date

### Purpose

The `date` command displays the current system date and can also change it.

### Syntax

```cmd
date
```

### Example

```cmd
date
```

### Display Date Without Changing It

```cmd
date /t
```

### Important Note

Running `date` without `/t` may prompt you to enter a new date.

Changing the system date can affect applications and scheduled operations. Administrator permissions may be required.

---

## 9. TIME — Display or Change Time

### Purpose

The `time` command displays or changes the system time.

### Syntax

```cmd
time
```

### Example

```cmd
time
```

### Display Time Without Changing It

```cmd
time /t
```

### Important Note

Running `time` without `/t` may prompt you to enter a new time.

Changing the system clock can affect scheduled operations, logs and applications.

---

## 10. COLOR — Change CMD Colors

### Purpose

The `color` command changes the foreground and background colors of the CMD window.

### Syntax

```cmd
color [attribute]
```

The attribute contains two hexadecimal characters:

- First character: Background color.
- Second character: Text color.

### Color Codes

| Code | Color |
|---|---|
| 0 | Black |
| 1 | Blue |
| 2 | Green |
| 3 | Aqua |
| 4 | Red |
| 5 | Purple |
| 6 | Yellow |
| 7 | White |
| 8 | Gray |
| 9 | Light Blue |
| A | Light Green |
| B | Light Aqua |
| C | Light Red |
| D | Light Purple |
| E | Light Yellow |
| F | Bright White |

### Examples

Green text on black background:

```cmd
color 0A
```

White text on blue background:

```cmd
color 17
```

Restore default colors:

```cmd
color
```

---

## 11. TITLE — Change CMD Window Title

### Purpose

The `title` command changes the title displayed in the CMD window.

### Syntax

```cmd
title [text]
```

### Example

```cmd
title Computer Science Learning
```

### Use Cases

- Identifying multiple terminal windows.
- Organizing command-line sessions.
- Customizing batch scripts.

---

## 12. PROMPT — Customize Command Prompt

### Purpose

The `prompt` command changes the appearance of the command prompt.

### Syntax

```cmd
prompt [text]
```

### Common Prompt Special Codes

| Code | Meaning |
|---|---|
| `$P` | Current drive and path |
| `$G` | Greater-than symbol |
| `$L` | Less-than symbol |
| `$D` | Current date |
| `$T` | Current time |
| `$N` | Current drive |
| `$V` | Windows version |
| `$$` | Dollar sign |
| `$S` | Space |
| `$+` | Plus sign based on PUSHD directory stack depth |

### Examples

Default-style prompt:

```cmd
prompt $P$G
```

Show only a greater-than sign:

```cmd
prompt $G
```

Show current path and time:

```cmd
prompt $T $P$G
```

Restore the default prompt:

```cmd
prompt
```

---

## 13. EXIT — Close CMD

### Purpose

The `exit` command terminates the current CMD command interpreter.

### Syntax

```cmd
exit
```

### Example

```cmd
exit
```

### Additional Option

```cmd
exit /b
```

`exit /b` exits the current batch script or subroutine without necessarily closing the parent CMD session.

An optional exit code can be supplied:

```cmd
exit /b 0
```

Here, `0` conventionally indicates successful completion.

---

## 14. START — Launch Applications

### Purpose

The `start` command opens a separate Command Prompt window, launches an application or opens a document using its associated application.

### Syntax

```cmd
start [options] ["title"] [command or program] [arguments]
```

### Examples

Open Notepad:

```cmd
start notepad
```

Open Calculator:

```cmd
start calc
```

Open a website:

```cmd
start https://www.google.com
```

Open another CMD window:

```cmd
start cmd
```

### Important Option

Open a program in a maximized window:

```cmd
start /max notepad
```

Open a program in a minimized window:

```cmd
start /min notepad
```

### Important Note

The first quoted argument to `start` is interpreted as the window title. When launching a quoted executable path, an empty title may be necessary.

Example:

```cmd
start "" "C:\Windows\System32\notepad.exe"
```

---

## 15. DOSKEY — Command History and Macros

### Purpose

`doskey` is a command-line utility that provides command history and macro functionality.

### Display Command History

```cmd
doskey /history
```

### Create a Macro

```cmd
doskey hello=echo Hello World
```

Now execute:

```cmd
hello
```

Output:

```text
Hello World
```

### Display Defined Macros

```cmd
doskey /macros
```

### Use Cases

- Reusing frequently entered commands.
- Creating command shortcuts.
- Improving command-line productivity.

Note: DOSKEY macros are session-specific unless configured again in a new session.

---

## 16. SHUTDOWN — Manage System Power Operations

### Purpose

The `shutdown` command allows users to shut down or restart Windows.

### Common Syntax

```cmd
shutdown [options]
```

### Important Options

| Option | Meaning |
|---|---|
| `/s` | Shut down the computer |
| `/r` | Restart the computer |
| `/a` | Abort a pending shutdown |
| `/t` | Set a time delay in seconds |
| `/l` | Log off the current user |
| `/h` | Hibernate the computer |
| `/f` | Force running applications to close |

### Examples

Schedule shutdown after 60 seconds:

```cmd
shutdown /s /t 60
```

Schedule restart after 60 seconds:

```cmd
shutdown /r /t 60
```

Cancel a pending shutdown:

```cmd
shutdown /a
```

Log off:

```cmd
shutdown /l
```

### Important Warning

Shutdown commands can interrupt work and cause unsaved data loss.

The `/f` option can force applications to close without saving their data. Use these commands carefully.

---

## 17. Quick Reference Table

| Command | Purpose |
|---|---|
| `help` | Display available commands |
| `cls` | Clear screen |
| `ver` | Display Windows version |
| `whoami` | Display current user |
| `hostname` | Display computer name |
| `echo` | Display text or variables |
| `date` | Display or change date |
| `time` | Display or change time |
| `color` | Change CMD colors |
| `title` | Change window title |
| `prompt` | Customize command prompt |
| `exit` | Close CMD |
| `start` | Launch programs |
| `doskey` | Manage command history and macros |
| `shutdown` | Shut down or restart Windows |

---

## 18. Important Concepts to Remember

1. `/?` displays command-specific help for many Windows commands.
2. `help` lists internal commands and other available command information.
3. `echo` can display environment variables.
4. `whoami` helps identify the current user.
5. `hostname` identifies the computer.
6. `prompt` customizes the command prompt.
7. `doskey` provides command history and macros.
8. `start` launches programs and other commands.
9. `shutdown` manages system power operations.
10. Commands that modify system settings may require elevated privileges.

---

## 19. Official Documentation

- [Windows Commands Reference](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [HELP](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/help)
- [ECHO](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/echo)
- [START](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/start)
- [DOSKEY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/doskey)
- [SHUTDOWN](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/shutdown)

---

**END OF LESSON 02 — CMD BASIC COMMANDS**
