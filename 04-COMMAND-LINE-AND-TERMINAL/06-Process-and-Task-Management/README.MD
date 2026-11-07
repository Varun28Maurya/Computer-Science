
# Lesson 06: Process and Task Management in Windows CMD

> **Module:** Command Line and Terminal  
> **Topic:** Windows Command Prompt (CMD)  
> **Lesson:** 06 — Process and Task Management  
> **Level:** Beginner to Advanced

---

# 1. Introduction

Process management is the process of monitoring and controlling programs currently running on a computer.

Whenever you open an application, execute a command, or start a background service, Windows creates or uses one or more processes.

Using CMD, you can:

- Display running processes.
- Identify Process IDs (PIDs).
- Find a particular application.
- Terminate unresponsive applications.
- Start programs.
- Manage Windows services.
- Inspect process information.
- Monitor application execution.
- Work with background processes.
- Understand process priorities.

These concepts are important for:

- Operating Systems.
- System Administration.
- Software Development.
- Debugging.
- Cybersecurity.
- Performance Troubleshooting.

---

# 2. Understanding Processes

## 2.1 What Is a Process?

A process is a program currently being executed by the operating system.

For example, when you open Google Chrome, Windows runs one or more Chrome processes.

Similarly:

| Application | Possible Process Name |
|---|---|
| Google Chrome | `chrome.exe` |
| Notepad | `notepad.exe` |
| Windows Explorer | `explorer.exe` |
| Command Prompt | `cmd.exe` |
| Python | `python.exe` |
| Node.js | `node.exe` |
| Visual Studio Code | `Code.exe` |

A single application can create multiple processes.

## 2.2 Program vs Process

| Program | Process |
|---|---|
| A set of instructions stored on disk | An executing instance of a program |
| Passive | Active |
| Stored as an executable or application files | Managed by the operating system |
| Does not necessarily consume CPU while inactive | May consume CPU and memory |

Example:

`notepad.exe` stored on your computer is a program.

When you open Notepad, Windows creates a process to execute it.

## 2.3 What Is a PID?

PID stands for Process Identifier.

It is a numerical identifier assigned to a process by Windows.

Example:

```text
Image Name          PID
========================
notepad.exe        4520
chrome.exe         6784
explorer.exe       1200
```

The numbers above are illustrative.

A PID helps Windows and administrators identify a specific running process.

## 2.4 What Is a Parent Process?

A parent process is a process that creates another process.

The newly created process is called a child process.

Example:

```text
cmd.exe
   |
   +--- python.exe
   |
   +--- node.exe
   |
   +--- notepad.exe
```

This is a simplified illustration of process creation.

---

# 3. TASKLIST — Display Running Processes

The `tasklist` command displays currently running processes.

Syntax:

```cmd
tasklist [options]
```

Display all running processes:

```cmd
tasklist
```

Example output:

```text
Image Name                     PID
========================= ========
System Idle Process              0
System                           4
explorer.exe                  1200
notepad.exe                   4520
chrome.exe                    6784
```

Actual output varies by system.

## 3.1 Display Detailed Process Information

```cmd
tasklist /v
```

The `/v` option displays verbose information.

## 3.2 Display Process Services

```cmd
tasklist /svc
```

Displays services associated with each process.

This is particularly useful when investigating Windows services hosted by processes such as `svchost.exe`.

## 3.3 Display Processes in List Format

```cmd
tasklist /fo list
```

## 3.4 Display Processes in CSV Format

```cmd
tasklist /fo csv
```

Save process information:

```cmd
tasklist /fo csv > processes.csv
```

## 3.5 Display Processes Without Column Headers

```cmd
tasklist /nh
```

## 3.6 Display Processes on a Remote Computer

```cmd
tasklist /s COMPUTERNAME
```

This attempts to query processes on a remote computer.

Remote access requires suitable permissions and network configuration.

---

# 4. Filtering Processes

The `/fi` option allows you to filter the output of `tasklist`.

Syntax:

```cmd
tasklist /fi "filter"
```

## 4.1 Filter by Process Name

```cmd
tasklist /fi "imagename eq notepad.exe"
```

Displays Notepad processes.

## 4.2 Filter by PID

```cmd
tasklist /fi "pid eq 4520"
```

Displays the process with PID 4520.

## 4.3 Filter by Memory Usage

```cmd
tasklist /fi "memusage gt 100000"
```

Displays processes using more than 100,000 KB of memory.

## 4.4 Filter by Status

```cmd
tasklist /fi "status eq running"
```

Filters processes based on their status.

## 4.5 Filter by Username

```cmd
tasklist /fi "username eq DESKTOP\Varun"
```

Replace the example username with the actual account name.

## 4.6 Combine Filtering and Output Formatting

```cmd
tasklist /fi "imagename eq chrome.exe" /fo table
```

### Important Filter Operators

| Operator | Meaning |
|---|---|
| `eq` | Equal |
| `ne` | Not equal |
| `gt` | Greater than |
| `lt` | Less than |
| `ge` | Greater than or equal |
| `le` | Less than or equal |

---

# 5. TASKKILL — Terminate Processes

The `taskkill` command terminates running processes.

Syntax:

```cmd
taskkill [options]
```

## 5.1 Terminate a Process by Name

```cmd
taskkill /im notepad.exe
```

Terminates a process named `notepad.exe`.

## 5.2 Forcefully Terminate a Process

```cmd
taskkill /f /im notepad.exe
```

The `/f` option requests forceful termination.

Use this when an application is not responding, but remember that unsaved work may be lost.

## 5.3 Terminate a Process Using PID

```cmd
taskkill /pid 4520
```

Terminates the process with PID 4520.

## 5.4 Forcefully Terminate a Process Using PID

```cmd
taskkill /f /pid 4520
```

## 5.5 Terminate a Process and Its Child Processes

```cmd
taskkill /f /t /pid 4520
```

The `/t` option terminates the specified process and its child processes.

## 5.6 Terminate Multiple Processes

```cmd
taskkill /im notepad.exe /im calculator.exe
```

Terminates matching processes.

## 5.7 Terminate Processes Using Filters

```cmd
taskkill /fi "imagename eq notepad.exe"
```

### Important TASKKILL Options

| Option | Description |
|---|---|
| `/im` | Specify process image name |
| `/pid` | Specify process ID |
| `/f` | Force termination |
| `/t` | Terminate child processes |
| `/fi` | Apply a filter |
| `/s` | Specify a remote computer |
| `/u` | Specify a user account |
| `/p` | Specify a password when required |

**WARNING:** Never terminate an unknown Windows system process just because its name looks unfamiliar.

---

# 6. START — Launch Applications

The `start` command launches applications, opens files, or starts commands in another command window.

Syntax:

```cmd
start [options] [title] [command]
```

## 6.1 Open Notepad

```cmd
start notepad
```

## 6.2 Open Calculator

```cmd
start calc
```

## 6.3 Open File Explorer

```cmd
start explorer
```

## 6.4 Open a Specific Directory

```cmd
start explorer "C:\Users\Varun\Documents"
```

## 6.5 Open a Website

```cmd
start https://www.google.com
```

This opens the URL using the default browser.

## 6.6 Open a File with Its Default Application

```cmd
start "" "C:\Users\Varun\Documents\notes.txt"
```

The first empty quotation marks represent the window title.

This is important when the target path itself contains spaces.

## 6.7 Start a Program with a Priority

```cmd
start /low notepad
```

The `/low` option starts the program with low process priority.

### Important START Options

| Option | Description |
|---|---|
| `/min` | Start minimized |
| `/max` | Start maximized |
| `/wait` | Wait for the launched process to finish |
| `/b` | Start without creating a new command window |
| `/low` | Start with low priority |
| `/normal` | Start with normal priority |
| `/high` | Start with high priority |
| `/realtime` | Request real-time priority |
| `/d` | Specify the starting directory |

**Warning:** Avoid `/realtime`. Giving an application real-time priority can interfere with system responsiveness.

---

# 7. Understanding Process Priorities

Windows uses process priority to influence how CPU scheduling resources are allocated.

A higher priority does not guarantee faster execution.

## 7.1 Common Priority Classes

| Priority Class | Meaning |
|---|---|
| Idle | Very low priority |
| Below Normal | Below normal priority |
| Normal | Standard priority |
| Above Normal | Above normal priority |
| High | High priority |
| Real Time | Highest priority class |

## 7.2 Start an Application with Low Priority

```cmd
start /low notepad
```

## 7.3 Start with Normal Priority

```cmd
start /normal notepad
```

## 7.4 Start with High Priority

```cmd
start /high notepad
```

## 7.5 Start with Above Normal Priority

```cmd
start /abovenormal notepad
```

**Important:** Priority affects scheduling decisions. It does not increase the physical processing power of the CPU.

---

# 8. TIMEOUT — Pause Command Execution

The `timeout` command pauses command execution for a specified number of seconds.

Syntax:

```cmd
timeout /t seconds
```

Example:

```cmd
timeout /t 10
```

Waits for 10 seconds.

## 8.1 Pause Without Allowing Keyboard Interruption

```cmd
timeout /t 10 /nobreak
```

The `/nobreak` option prevents a key press from ending the wait early.

## 8.2 Skip the Wait

```cmd
timeout /t 0
```

### Important Options

| Option | Description |
|---|---|
| `/t` | Specify the waiting time |
| `/nobreak` | Ignore key presses |

---

# 9. SC — Service Control

Windows services are background programs that provide functionality to the operating system and applications.

Examples include:

- Windows Update.
- Print Spooler.
- Windows Time.
- Background Intelligent Transfer Service.

The `sc` command communicates with the Windows Service Control Manager.

Syntax:

```cmd
sc [command] [service_name]
```

## 9.1 Display Service Information

```cmd
sc query
```

Displays service information.

## 9.2 Query a Specific Service

```cmd
sc query spooler
```

Displays information about the Print Spooler service.

## 9.3 Query All Services

```cmd
sc query state= all
```

The space after `state=` is required in this syntax.

## 9.4 Display Service Configuration

```cmd
sc qc spooler
```

Displays the configuration of the specified service.

## 9.5 Start a Service

```cmd
sc start spooler
```

Requests that the Print Spooler service start.

## 9.6 Stop a Service

```cmd
sc stop spooler
```

Requests that the Print Spooler service stop.

Stopping a service can affect applications and Windows functionality.

## 9.7 Display Service Dependencies

```cmd
sc enumdepend spooler
```

Displays services that depend on the specified service.

### Important SC Commands

| Command | Purpose |
|---|---|
| `sc query` | Display service status |
| `sc qc` | Display service configuration |
| `sc start` | Start a service |
| `sc stop` | Stop a service |
| `sc config` | Modify service configuration |
| `sc enumdepend` | Display dependent services |
| `sc delete` | Delete a service registration |

**WARNING:** Do not casually modify, stop, or delete Windows services. Some services are required for normal system operation.

---

# 10. SC CONFIG — Configure Services

The `sc config` command modifies a service's configuration.

Example:

```cmd
sc config spooler start= demand
```

This configures the Print Spooler service for manual startup.

Common startup configuration values:

| Value | Meaning |
|---|---|
| `boot` | Boot-start |
| `system` | System-start |
| `auto` | Automatic |
| `demand` | Manual |
| `disabled` | Disabled |

Example:

```cmd
sc config spooler start= auto
```

**Important:** There must be a space after `start=`.

Service configuration changes generally require Administrator privileges.

Do not change service startup types without understanding the impact.

---

# 11. SERVICES.MSC — Graphical Service Manager

Windows also provides a graphical interface for managing services.

Open it using:

```cmd
services.msc
```

This opens the Services management console.

You can use it to:

- View installed services.
- Check service status.
- Start services.
- Stop services.
- Restart services.
- Modify startup types.
- Inspect service descriptions.

The graphical interface can be easier to understand when learning Windows services.

---

# 12. WMIC — Process Information

WMIC stands for Windows Management Instrumentation Command-line.

It was historically used to query Windows management information.

**Important:** WMIC is deprecated and may not be available in modern Windows installations.

Example:

```cmd
wmic process list brief
```

This displays a brief process listing on systems where WMIC is available.

Display process names and PIDs:

```cmd
wmic process get name,processid
```

Display executable paths:

```cmd
wmic process get name,executablepath
```

Display parent process IDs:

```cmd
wmic process get name,processid,parentprocessid
```

### Modern PowerShell Alternatives

Display processes:

```cmd
powershell -NoProfile -Command "Get-Process"
```

Display process names and IDs:

```cmd
powershell -NoProfile -Command "Get-Process | Select-Object ProcessName,Id"
```

Display parent process IDs:

```cmd
powershell -NoProfile -Command "Get-CimInstance Win32_Process | Select-Object Name,ProcessId,ParentProcessId"
```

These are PowerShell commands launched from CMD, not native CMD commands.

---

# 13. FINDSTR — Search Process Output

The `findstr` command searches text using strings and patterns.

It is useful when filtering output from process-management commands.

## 13.1 Search for a Process

```cmd
tasklist | findstr "chrome"
```

## 13.2 Ignore Case

```cmd
tasklist | findstr /i "chrome"
```

## 13.3 Search for Multiple Names

```cmd
tasklist | findstr /i "chrome python node"
```

## 13.4 Display Matching Line Numbers

```cmd
tasklist | findstr /n /i "chrome"
```

### Important FINDSTR Options

| Option | Description |
|---|---|
| `/i` | Ignore case |
| `/n` | Display line numbers |
| `/r` | Use regular expressions |
| `/c:"text"` | Search for an exact string |
| `/v` | Display lines that do not match |
| `/m` | Display filenames containing matches |

---

# 14. START vs CALL vs CMD

These commands are useful when executing programs and scripts.

## START

Launches a program or command in another process context.

Example:

```cmd
start notepad
```

## CALL

Calls another batch file and returns to the current batch script after it finishes.

Example:

```cmd
call second.bat
```

## CMD

Starts a new command interpreter.

Example:

```cmd
cmd
```

Start a new CMD session and execute a command:

```cmd
cmd /c "echo Hello"
```

The `/c` option executes the command and then exits.

Start a new CMD session that remains open:

```cmd
cmd /k "echo Hello"
```

The `/k` option executes the command and keeps the new CMD session open.

### Comparison

| Command | Purpose |
|---|---|
| `start` | Launch a program or command |
| `call` | Call another batch script |
| `cmd /c` | Execute a command and exit |
| `cmd /k` | Execute a command and remain open |

---

# 15. Process Management Quick Reference

| Command | Purpose |
|---|---|
| `tasklist` | Display running processes |
| `taskkill` | Terminate processes |
| `start` | Launch programs |
| `timeout` | Pause execution |
| `sc query` | Display service information |
| `sc start` | Start a service |
| `sc stop` | Stop a service |
| `sc qc` | Display service configuration |
| `sc config` | Modify service configuration |
| `services.msc` | Open graphical service manager |
| `findstr` | Search command output |
| `cmd /c` | Execute and exit |
| `cmd /k` | Execute and remain open |
| `call` | Call another batch script |

---

# 16. Important Command Comparisons

## 16.1 TASKLIST vs TASKKILL

| TASKLIST | TASKKILL |
|---|---|
| Displays running processes | Terminates running processes |
| Helps identify PIDs | Uses process names or PIDs |
| Read-oriented operation | Changes system process state |

## 16.2 Process vs Service

| Process | Service |
|---|---|
| Running instance of a program | Background component managed by Windows Service Control Manager |
| Identified by a PID | Identified by a service name |
| Can be foreground or background | Typically runs in the background |
| Inspected using `tasklist` | Inspected using `sc query` |

A service usually runs inside a process, but one process can host multiple services.

## 16.3 START vs TASKKILL

| START | TASKKILL |
|---|---|
| Launches programs | Terminates processes |
| Starts new execution | Stops existing execution |

---

# 17. Common Errors and Troubleshooting

## Error 1: Access is denied

Possible causes:

- Insufficient permissions.
- The process belongs to another user.
- The process is protected.
- The requested service operation requires elevation.

Possible solution:

Run CMD as Administrator only when necessary.

## Error 2: The process could not be found

Possible causes:

- Incorrect process name.
- Incorrect PID.
- The process has already terminated.
- The application is not running.

Check:

```cmd
tasklist
```

## Error 3: The service name is invalid

Possible causes:

- Incorrect service name.
- The service is not installed.
- The display name was used instead of the service name.

Inspect service names:

```cmd
sc query state= all
```

## Error 4: The service cannot be started

Possible causes:

- Required dependencies are unavailable.
- The service is disabled.
- Insufficient permissions.
- The service encountered an internal error.

Inspect its configuration:

```cmd
sc qc ServiceName
```

## Error 5: Application does not launch

Possible causes:

- Application is not installed.
- Executable is not available through PATH.
- Incorrect executable name.
- Invalid file path.

Check executable availability:

```cmd
where application_name
```

---

# 18. Important Safety Guidelines

1. Verify the process name and PID before terminating a process.
2. Avoid terminating unfamiliar Windows system processes.
3. Do not use forceful termination unnecessarily.
4. Remember that forceful termination may result in lost unsaved work.
5. Do not stop important Windows services without understanding their purpose.
6. Avoid changing service startup configurations casually.
7. Do not use real-time priority for ordinary applications.
8. Use Administrator mode only when required.
9. Never execute process-management commands copied from unknown sources without understanding them.
10. Remember that one application may create multiple processes.

---

# 19. Key Takeaways

After studying this lesson, you should understand:

- What a process is.
- The difference between a program and a process.
- What a Process ID (PID) represents.
- Parent and child processes.
- How to inspect processes using `tasklist`.
- How to filter processes.
- How to terminate processes using `taskkill`.
- How to launch applications using `start`.
- How process priority works.
- How to pause command execution using `timeout`.
- How Windows services work.
- How to inspect and manage services using `sc`.
- How to use `services.msc`.
- How to inspect process information using WMIC and PowerShell alternatives.
- How to filter command output using `findstr`.

---

# 20. Official Microsoft Documentation

- [TASKLIST](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist)
- [TASKKILL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/taskkill)
- [START](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/start)
- [TIMEOUT](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/timeout)
- [SC](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc)
- [CMD](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmd)
- [CALL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/call)
- [FINDSTR](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/findstr)

---

**End of Lesson 06 — Process and Task Management in Windows CMD**
