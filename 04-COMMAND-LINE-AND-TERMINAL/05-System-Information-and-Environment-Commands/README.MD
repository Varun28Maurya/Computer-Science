
# Lesson 05: System Information and Environment Commands in Windows CMD

> **Module:** Command Line and Terminal  
> **Topic:** Windows Command Prompt (CMD)  
> **Lesson:** 05 — System Information and Environment Commands  
> **Level:** Beginner to Advanced

---

# 1. Introduction

System information commands help you understand the configuration and current state of your computer.

Using these commands, you can:

- Identify your Windows version.
- Display computer and user information.
- Inspect hardware and operating system details.
- Check environment variables.
- Understand the PATH variable.
- Locate executable files.
- Inspect installed drivers.
- View system configuration.
- Check system uptime.
- Inspect system architecture.

These commands are useful for:

- System administration.
- Software development.
- Debugging.
- Troubleshooting.
- Network administration.
- Understanding Windows internals.

---

# 2. VER — Display Windows Version

The `ver` command displays the Windows version information reported by the command interpreter.

Syntax:

```cmd
ver
```

Example:

```text
Microsoft Windows [Version 10.0.xxxxx.xxxx]
```

The exact output depends on your Windows installation.

### Important Points

- `ver` displays version information.
- It does not provide a complete Windows edition or hardware report.
- Use `systeminfo` for more detailed information.

---

# 3. SYSTEMINFO — Display System Information

The `systeminfo` command displays detailed information about the computer and operating system.

Syntax:

```cmd
systeminfo
```

It can display:

- Host name.
- Operating system name.
- Operating system version.
- Operating system manufacturer.
- System manufacturer.
- System model.
- System type.
- Processor information.
- BIOS information.
- Windows installation date.
- Last boot time.
- Available physical memory.
- Virtual memory information.
- Network adapter information.
- Installed hotfixes.

Example:

```cmd
systeminfo
```

Sample output:

```text
Host Name:                 DESKTOP-ABC123
OS Name:                   Microsoft Windows 11 Pro
OS Version:                10.0.xxxxx N/A Build xxxxx
OS Manufacturer:           Microsoft Corporation
System Manufacturer:       Dell Inc.
System Model:              Example Model
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
Total Physical Memory:     16,384 MB
```

The values above are illustrative.

## 3.1 Save System Information to a File

```cmd
systeminfo > system-report.txt
```

This saves the command output to a text file.

## 3.2 Display System Information Page by Page

```cmd
systeminfo | more
```

## 3.3 Find Specific Information

Search for the operating system name:

```cmd
systeminfo | findstr /i "OS Name"
```

Search for processor information:

```cmd
systeminfo | findstr /i "Processor"
```

Search for memory information:

```cmd
systeminfo | findstr /i "Memory"
```

### Important Note

The output format and available fields can vary between Windows versions and system configurations.

---

# 4. HOSTNAME — Display Computer Name

The `hostname` command displays the computer's network host name.

Syntax:

```cmd
hostname
```

Example output:

```text
DESKTOP-ABC123
```

This is useful when identifying a computer on a local network.

**Important:** The hostname is not necessarily the same as the Windows user account name.

---

# 5. WHOAMI — Identify Current User

The `whoami` command displays the identity of the currently logged-in user.

Syntax:

```cmd
whoami
```

Example output:

```text
desktop-abc123\varun
```

## 5.1 Display User Information

```cmd
whoami /user
```

Displays the current user's security identifier (SID).

## 5.2 Display Group Membership

```cmd
whoami /groups
```

Displays the security groups associated with the current user.

## 5.3 Display Privileges

```cmd
whoami /priv
```

Displays the privileges associated with the current access token.

## 5.4 Display All Available Information

```cmd
whoami /all
```

Displays user, group, and privilege information.

### Important WHOAMI Options

| Option | Description |
|---|---|
| `/user` | Display user SID |
| `/groups` | Display security groups |
| `/priv` | Display privileges |
| `/all` | Display all available security information |
| `/fo` | Specify output format |

---

# 6. SET — Display Environment Variables

Environment variables are named values maintained by Windows and applications.

They store information such as:

- Windows directory.
- User profile directory.
- Temporary file locations.
- Executable search paths.
- Application configuration.

The `set` command displays or modifies environment variables in the current CMD environment.

Syntax:

```cmd
set
```

This displays environment variables available to the current command session.

Example output:

```text
COMPUTERNAME=DESKTOP-ABC123
HOMEDRIVE=C:
HOMEPATH=\Users\Varun
OS=Windows_NT
PROCESSOR_ARCHITECTURE=AMD64
TEMP=C:\Users\Varun\AppData\Local\Temp
USERNAME=Varun
```

Actual values vary by computer.

## 6.1 Display a Specific Variable

```cmd
echo %USERNAME%
```

Displays the current username.

```cmd
echo %COMPUTERNAME%
```

Displays the computer name.

```cmd
echo %USERPROFILE%
```

Displays the current user's profile directory.

```cmd
echo %TEMP%
```

Displays the temporary directory.

```cmd
echo %WINDIR%
```

Displays the Windows installation directory.

```cmd
echo %SYSTEMROOT%
```

Displays the Windows system root directory.

## 6.2 Create an Environment Variable

```cmd
set PROJECT=ComputerScience
```

This creates a variable named `PROJECT` in the current CMD session.

Display it:

```cmd
echo %PROJECT%
```

Output:

```text
ComputerScience
```

## 6.3 Change an Environment Variable

```cmd
set PROJECT=Programming
```

The previous value is replaced.

## 6.4 Delete an Environment Variable

```cmd
set PROJECT=
```

This removes the variable from the current CMD environment.

## 6.5 Search for Environment Variables

```cmd
set PATH
```

Displays variables whose names begin with `PATH`.

### Important SET Behavior

Variables created using `set` are normally limited to the current CMD process and its child processes.

They do not automatically become permanent Windows environment variables.

---

# 7. PATH — Environment Search Path

The PATH environment variable contains a list of directories where Windows searches for executable commands.

For example, when you execute:

```cmd
python
```

Windows searches the configured command locations for an appropriate executable.

## 7.1 Display PATH

```cmd
echo %PATH%
```

This displays the PATH variable.

It may contain directories such as:

```text
C:\Windows\System32
C:\Windows
C:\Program Files\Python
```

The actual list depends on your computer.

## 7.2 Temporarily Add a Directory to PATH

```cmd
set PATH=%PATH%;C:\MyTools
```

This adds `C:\MyTools` to PATH for the current CMD session.

## 7.3 Temporarily Replace PATH

```cmd
set PATH=C:\MyTools
```

**WARNING:** This replaces the PATH variable in the current session. Windows may no longer find commands located in other directories.

## 7.4 Permanently Modify PATH

Windows provides persistent environment-variable settings.

You can open the graphical Environment Variables interface using:

```cmd
sysdm.cpl
```

Then:

1. Open the Advanced tab.
2. Select Environment Variables.
3. Locate the appropriate PATH variable.
4. Edit it carefully.
5. Save the changes.

User PATH applies to the current user, while System PATH applies more broadly.

Changes normally affect newly opened processes, not already-running CMD sessions.

---

# 8. WHERE — Locate Executable Files

The `where` command locates files matching a search pattern.

It is commonly used to find executables available through PATH.

Syntax:

```cmd
where [options] pattern
```

## 8.1 Locate Python

```cmd
where python
```

This displays matching Python executable locations found through the search path.

## 8.2 Locate Git

```cmd
where git
```

## 8.3 Locate Node.js

```cmd
where node
```

## 8.4 Locate Multiple Commands

```cmd
where python node git
```

## 8.5 Search in a Specific Directory

```cmd
where C:\Windows\System32\cmd.exe
```

## 8.6 Search Recursively

```cmd
where /r C:\Windows cmd.exe
```

This searches recursively under the specified directory.

### Important WHERE Options

| Option | Description |
|---|---|
| `/r` | Search recursively |
| `/q` | Quiet mode |
| `/f` | Display filenames in quotation marks |
| `/t` | Display file size and modification date |

### WHERE vs FIND

| WHERE | FIND |
|---|---|
| Locates files | Searches for text inside files |
| Commonly used for executable discovery | Commonly used for text searching |
| Searches PATH by default | Searches file contents |

---

# 9. DRIVERQUERY — Display Installed Drivers

The `driverquery` command displays installed device drivers.

Syntax:

```cmd
driverquery
```

It can display:

- Driver module name.
- Display name.
- Driver type.
- Link date.

## 9.1 Display Detailed Driver Information

```cmd
driverquery /v
```

Displays verbose driver information.

## 9.2 Display Drivers in List Format

```cmd
driverquery /fo list
```

## 9.3 Display Drivers in Table Format

```cmd
driverquery /fo table
```

## 9.4 Display Drivers in CSV Format

```cmd
driverquery /fo csv
```

## 9.5 Save Driver Information

```cmd
driverquery /fo csv > drivers.csv
```

This saves driver information in CSV format.

### Important DRIVERQUERY Options

| Option | Description |
|---|---|
| `/v` | Verbose output |
| `/fo` | Select output format |
| `/si` | Display signed driver information |

**Note:** Displaying driver information does not install, update, or repair drivers.

---

# 10. TASKLIST — Display Running Processes

The `tasklist` command displays currently running processes.

A process is an instance of a running program.

Syntax:

```cmd
tasklist
```

Example output:

```text
Image Name                     PID
========================= ========
explorer.exe                  1234
chrome.exe                    5678
notepad.exe                   9012
```

The process IDs shown are illustrative.

## 10.1 Display Detailed Process Information

```cmd
tasklist /v
```

## 10.2 Display Services Associated with Processes

```cmd
tasklist /svc
```

## 10.3 Filter by Process Name

```cmd
tasklist /fi "imagename eq notepad.exe"
```

## 10.4 Filter by Process ID

```cmd
tasklist /fi "pid eq 1234"
```

## 10.5 Save Process Information

```cmd
tasklist > processes.txt
```

### Important TASKLIST Options

| Option | Description |
|---|---|
| `/v` | Display verbose information |
| `/svc` | Display services hosted by each process |
| `/fi` | Apply a filter |
| `/fo` | Specify output format |
| `/nh` | Remove column headers |

---

# 11. TASKKILL — Terminate Processes

The `taskkill` command terminates running processes.

Syntax:

```cmd
taskkill [options]
```

## 11.1 Terminate a Process by Name

```cmd
taskkill /im notepad.exe
```

## 11.2 Forcefully Terminate a Process

```cmd
taskkill /f /im notepad.exe
```

The `/f` option requests forceful termination.

## 11.3 Terminate a Process Using PID

```cmd
taskkill /pid 1234
```

## 11.4 Terminate a Process and Its Child Processes

```cmd
taskkill /f /t /pid 1234
```

### Important TASKKILL Options

| Option | Description |
|---|---|
| `/im` | Specify process image name |
| `/pid` | Specify process ID |
| `/f` | Force termination |
| `/t` | Terminate child processes |
| `/fi` | Apply a filter |

**WARNING:** Terminating a process can cause unsaved work to be lost. Avoid terminating Windows system processes unless you understand their purpose.

---

# 12. SETX — Create Persistent Environment Variables

The `setx` command creates or modifies persistent environment variables.

Unlike `set`, its changes are stored for future command sessions.

Syntax:

```cmd
setx variable_name value
```

## 12.1 Create a Persistent User Variable

```cmd
setx PROJECT_HOME "C:\Projects"
```

This creates a persistent user environment variable.

## 12.2 Display the Variable

Open a new CMD window and execute:

```cmd
echo %PROJECT_HOME%
```

The new CMD window is important because `setx` does not update the environment of the current CMD process.

## 12.3 Create a System Environment Variable

```cmd
setx PROJECT_HOME "C:\Projects" /m
```

The `/m` option targets the system environment rather than the current user's environment.

This generally requires Administrator privileges.

### SET vs SETX

| Feature | SET | SETX |
|---|---|---|
| Changes current CMD environment | Yes | No |
| Persists after closing CMD | No | Yes |
| Affects future command sessions | No | Yes |
| Can modify user variables | Current process environment | Yes |
| Can modify system variables | No, not persistently | Yes, with `/m` and appropriate permissions |

**Important SETX Warnings:**

- Changes are not reflected in the current CMD session.
- Be careful when modifying PATH using SETX.
- Do not casually replace the existing PATH value.
- Older Windows versions and command environments may impose length limitations.

---

# 13. PROMPT — Change the Command Prompt Display

The `prompt` command changes how the CMD prompt appears.

Syntax:

```cmd
prompt [text]
```

Example:

```cmd
prompt MyCMD$G
```

The prompt becomes:

```text
MyCMD>
```

## Common PROMPT Special Codes

| Code | Meaning |
|---|---|
| `$A` | `&` |
| `$B` | `|` |
| `$C` | `(` |
| `$D` | Current date |
| `$E` | Escape character |
| `$F` | `)` |
| `$G` | `>` |
| `$H` | Backspace |
| `$L` | `<` |
| `$N` | Current drive |
| `$P` | Current drive and path |
| `$Q` | `=` |
| `$S` | Space |
| `$T` | Current time |
| `$_` | New line |
| `$$` | `$` |

Display the current drive and directory:

```cmd
prompt $P$G
```

Display the date and time:

```cmd
prompt $D $T$G
```

Restore the default prompt:

```cmd
prompt
```

---

# 14. DATE and TIME — Display and Set System Date and Time

## DATE

Display or change the system date:

```cmd
date
```

Display the date without prompting for a change:

```cmd
date /t
```

## TIME

Display or change the system time:

```cmd
time
```

Display the time without prompting for a change:

```cmd
time /t
```

**Important:** Changing the system date or time may require additional permissions and can affect applications and scheduled tasks.

---

# 15. Managing Command Output

CMD supports redirection and pipes, which are useful for saving and filtering system information.

## 15.1 Save System Information

```cmd
systeminfo > system-info.txt
```

## 15.2 Append Process Information

```cmd
tasklist >> system-info.txt
```

## 15.3 Search for a Specific Process

```cmd
tasklist | findstr /i "chrome"
```

## 15.4 Display Only Matching Driver Information

```cmd
driverquery | findstr /i "display"
```

## 15.5 Display Long Output Page by Page

```cmd
systeminfo | more
```

---

# 16. Important System Environment Variables

Windows provides many predefined environment variables.

| Variable | Purpose |
|---|---|
| `%USERNAME%` | Current username |
| `%USERPROFILE%` | Current user's profile directory |
| `%COMPUTERNAME%` | Computer name |
| `%WINDIR%` | Windows directory |
| `%SYSTEMROOT%` | Windows system root |
| `%SYSTEMDRIVE%` | Drive containing Windows |
| `%TEMP%` | Current user's temporary directory |
| `%TMP%` | Temporary directory |
| `%HOMEDRIVE%` | User home drive |
| `%HOMEPATH%` | User home path |
| `%APPDATA%` | Roaming application data directory |
| `%LOCALAPPDATA%` | Local application data directory |
| `%PROGRAMFILES%` | Program Files directory |
| `%PROGRAMFILES(X86)%` | 32-bit Program Files directory on supported 64-bit Windows installations |
| `%PATH%` | Executable search path |
| `%OS%` | Operating system identifier |

Display a variable:

```cmd
echo %USERNAME%
```

Display the user profile:

```cmd
echo %USERPROFILE%
```

Display the Windows directory:

```cmd
echo %WINDIR%
```

---

# 17. Quick Reference Table

| Command | Purpose |
|---|---|
| `ver` | Display Windows version |
| `systeminfo` | Display detailed system information |
| `hostname` | Display computer name |
| `whoami` | Display current user identity |
| `set` | Display or modify current environment variables |
| `setx` | Create or modify persistent environment variables |
| `where` | Locate files and executables |
| `driverquery` | Display installed drivers |
| `tasklist` | Display running processes |
| `taskkill` | Terminate processes |
| `prompt` | Customize CMD prompt |
| `date` | Display or change system date |
| `time` | Display or change system time |
| `echo` | Display text or variable values |
| `findstr` | Search for matching text |
| `more` | Display output page by page |
| `sysdm.cpl` | Open System Properties |

---

# 18. Important Command Comparisons

## 18.1 SET vs SETX

- `set` modifies environment variables in the current CMD process.
- `setx` stores environment-variable changes for future processes.

## 18.2 WHERE vs PATH

- `where` searches for matching files.
- `PATH` is an environment variable containing directories used for executable lookup.

## 18.3 TASKLIST vs TASKKILL

- `tasklist` displays running processes.
- `taskkill` terminates processes.

## 18.4 VER vs SYSTEMINFO

- `ver` displays Windows version information.
- `systeminfo` displays a much broader system report.

## 18.5 HOSTNAME vs WHOAMI

- `hostname` displays the computer name.
- `whoami` displays the current user identity.

---

# 19. Common Errors and Troubleshooting

## Error 1: 'Command is not recognized'

Possible causes:

- The command is unavailable.
- Its executable directory is missing from PATH.
- The application is not installed.
- The command is misspelled.

Useful command:

```cmd
where python
```

## Error 2: Access is denied

Possible causes:

- Insufficient permissions.
- The command requires Administrator privileges.
- The requested resource is protected.

Use elevated CMD only when necessary.

## Error 3: Environment Variable Not Found

Example:

```cmd
echo %PROJECT_HOME%
```

If the variable has not been defined, CMD may display the variable expression itself.

Check current variables:

```cmd
set
```

## Error 4: SETX Change Not Visible

Remember that SETX does not update the current CMD process.

Open a new CMD window and check again.

## Error 5: WHERE Cannot Find a File

Possible causes:

- The application is not installed.
- Its directory is not in PATH.
- The executable has a different name.
- The file is outside the search locations.

---

# 20. Key Takeaways

After studying this lesson, you should understand:

- How to inspect Windows system information.
- How to identify the current user and computer.
- How to inspect environment variables.
- How PATH works.
- How to locate executables using WHERE.
- How to inspect installed drivers.
- How to list running processes.
- How to terminate processes.
- How to create persistent environment variables.
- How to customize the CMD prompt.
- How to save and filter system command output.

---

# 21. Official Microsoft Documentation

- [Windows Commands](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [SYSTEMINFO](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/systeminfo)
- [WHOAMI](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/whoami)
- [SET](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/set_1)
- [SETX](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/setx)
- [WHERE](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/where)
- [DRIVERQUERY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/driverquery)
- [TASKLIST](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist)
- [TASKKILL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/taskkill)
- [PROMPT](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/prompt)

---

**End of Lesson 05 — System Information and Environment Commands**
