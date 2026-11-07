
# Lesson 03: File and Directory Management in Windows CMD

> **Module:** Command Line and Terminal  
> **Topic:** Windows Command Prompt (CMD)  
> **Lesson:** 03 — File and Directory Management  
> **Level:** Beginner to Intermediate

---

## 1. Introduction

File and directory management is one of the most important skills when working with the Windows Command Prompt.

Using CMD, you can:

- Navigate between directories.
- Display files and folders.
- Create new directories.
- Create and view text files.
- Copy files and directories.
- Move files and directories.
- Rename files and directories.
- Delete files and directories.
- View directory structures.
- Inspect file attributes.

Before learning these commands, understand two basic terms.

### File

A file is a collection of data stored under a filename.

Examples:

```text
notes.txt
photo.jpg
program.py
index.html
report.pdf
```

### Directory

A directory is another name for a folder. It stores files and other directories.

Example:

```text
Documents/
├── Notes/
│   ├── chapter1.txt
│   └── chapter2.txt
├── Projects/
│   └── website.html
└── resume.pdf
```

---

# 2. Understanding File Paths

A path identifies the location of a file or directory.

Windows supports two important types of paths.

## 2.1 Absolute Path

An absolute path specifies the complete location of a file or directory, starting from a drive or network location.

Example:

```cmd
C:\Users\Varun\Documents\notes.txt
```

Another example:

```cmd
D:\Projects\Python\main.py
```

An absolute path does not depend on your current working directory.

## 2.2 Relative Path

A relative path specifies a location in relation to your current working directory.

Suppose your current directory is:

```text
C:\Users\Varun\Documents
```

A relative path could be:

```text
Projects\website.html
```

This refers to:

```text
C:\Users\Varun\Documents\Projects\website.html
```

## 2.3 Special Path Symbols

| Symbol | Meaning |
|---|---|
| `.` | Current directory |
| `..` | Parent directory |
| `\` | Root of the current drive |
| `C:\` | Root directory of drive C |

Examples:

```cmd
cd .
cd ..
cd \
```

## 2.4 Paths Containing Spaces

If a filename or directory contains spaces, enclose its path in double quotation marks.

Correct:

```cmd
cd "C:\Users\Varun\My Documents"
```

Incorrect:

```cmd
cd C:\Users\Varun\My Documents
```

Without quotation marks, CMD may interpret the path as multiple arguments.

---

# 3. Displaying Files and Directories

## 3.1 DIR — Display Directory Contents

The `dir` command displays files and directories in the current location.

Syntax:

```cmd
dir [path] [options]
```

Example:

```cmd
dir
```

Display contents of another directory:

```cmd
dir C:\Users\Varun\Documents
```

Display only directories:

```cmd
dir /ad
```

Display only files:

```cmd
dir /a-d
```

Display hidden files and directories:

```cmd
dir /a
```

Display files in a wide format:

```cmd
dir /w
```

Display filenames without additional details:

```cmd
dir /b
```

Display files in all subdirectories:

```cmd
dir /s
```

Display files sorted by name:

```cmd
dir /o:n
```

Display files sorted by size:

```cmd
dir /o:s
```

Display files sorted by modification date:

```cmd
dir /o:d
```

Combine options:

```cmd
dir /a /s /b
```

### Important DIR Options

| Option | Description |
|---|---|
| `/a` | Display files with all attributes |
| `/ad` | Display directories only |
| `/a-d` | Display files only |
| `/s` | Include subdirectories |
| `/b` | Bare format |
| `/w` | Wide listing format |
| `/o:n` | Sort by name |
| `/o:s` | Sort by size |
| `/o:d` | Sort by date |
| `/p` | Pause after each screen |
| `/q` | Display file ownership information |
| `/t:w` | Display last write time |

---

# 4. Navigating Between Directories

## 4.1 CD — Change Directory

The `cd` command changes the current working directory.

Syntax:

```cmd
cd [path]
```

Open a directory:

```cmd
cd Documents
```

Move into a nested directory:

```cmd
cd Documents\Projects
```

Move one directory backward:

```cmd
cd ..
```

Move two directories backward:

```cmd
cd ..\..
```

Move to the root of the current drive:

```cmd
cd \
```

Display the current directory:

```cmd
cd
```

## 4.2 CD /D — Change Drive and Directory

When switching drives, use `/d` to change both the drive and directory.

Example:

```cmd
cd /d D:\Projects
```

This changes the current drive to D and opens the Projects directory.

Without `/d`, changing to a directory on another drive does not necessarily change the active drive.

## 4.3 Switching Drives

To switch to drive D:

```cmd
D:
```

To switch to drive E:

```cmd
E:
```

---

# 5. Creating Directories

## 5.1 MD — Make Directory

The `md` command creates a new directory.

Syntax:

```cmd
md directory_name
```

Example:

```cmd
md Projects
```

Create a directory with spaces:

```cmd
md "My Projects"
```

Create nested directories:

```cmd
md Projects\WebDevelopment\HTML
```

CMD can create the intermediate directories in this path when they do not already exist.

## 5.2 MKDIR — Create Directory

`mkdir` is another name for `md`.

Example:

```cmd
mkdir Python
```

Both commands perform the same basic operation:

```cmd
md Python
mkdir Python
```

---

# 6. Removing Directories

## 6.1 RD — Remove Directory

The `rd` command removes a directory.

Syntax:

```cmd
rd directory_name
```

Example:

```cmd
rd OldFolder
```

By default, the directory must be empty.

## 6.2 RMDIR — Remove Directory

`rmdir` is another name for `rd`.

Example:

```cmd
rmdir OldFolder
```

## 6.3 Remove a Directory and Its Contents

Use `/s` to remove a directory and everything inside it.

```cmd
rd /s Projects
```

CMD asks for confirmation before deleting the directory tree.

To suppress confirmation, `/q` can be added:

```cmd
rd /s /q Projects
```

**WARNING:** This can permanently remove a directory and all its contents. It does not send the deleted files to the Recycle Bin.

Always verify the target path before using `/s` or `/q`.

---

# 7. Creating Files

CMD does not have a dedicated built-in command named `createfile`, but files can be created using commands such as `echo`, `copy con`, and `type`.

## 7.1 ECHO — Create a Text File

Create a file containing text:

```cmd
echo Hello World > hello.txt
```

The `>` operator creates the file if it does not exist.

If the file already exists, its previous contents are overwritten.

## 7.2 Append Content to a File

Use `>>` to append text without replacing existing contents.

```cmd
echo Welcome to CMD >> hello.txt
```

Difference:

| Operator | Meaning |
|---|---|
| `>` | Create or overwrite output |
| `>>` | Append output |

## 7.3 Create an Empty File Using NUL

```cmd
type nul > empty.txt
```

This creates an empty file.

If the file already exists, its contents are cleared.

## 7.4 Create a File Using COPY CON

The `copy con` command accepts keyboard input and writes it to a file.

```cmd
copy con notes.txt
```

Type your content:

```text
This is my first CMD file.
Learning Windows commands.
```

Press:

```text
Ctrl + Z
```

Then press Enter to finish and save.

---

# 8. Viewing File Contents

## 8.1 TYPE — Display File Contents

The `type` command displays the contents of a text file.

Syntax:

```cmd
type filename
```

Example:

```cmd
type notes.txt
```

Display multiple files:

```cmd
type file1.txt file2.txt
```

Display a file using its absolute path:

```cmd
type "C:\Users\Varun\Documents\notes.txt"
```

**Note:** `type` is intended for text files. Displaying binary files may produce unreadable output.

## 8.2 MORE — Display Content Page by Page

The `more` command displays long text output one screen at a time.

Example:

```cmd
more notes.txt
```

It can also receive output from another command through a pipe:

```cmd
dir /s | more
```

Common navigation:

| Key | Action |
|---|---|
| Space | Next page |
| Enter | Next line |
| Q | Quit |

## 8.3 FIND — Search for Text in Files

The `find` command searches for a specific text string inside a file.

Syntax:

```cmd
find "text" filename
```

Example:

```cmd
find "Hello" notes.txt
```

Display matching lines with line numbers:

```cmd
find /n "Hello" notes.txt
```

Display only the number of matching lines:

```cmd
find /c "Hello" notes.txt
```

Ignore uppercase and lowercase differences:

```cmd
find /i "hello" notes.txt
```

### Important FIND Options

| Option | Description |
|---|---|
| `/v` | Display lines that do not contain the text |
| `/c` | Display the count of matching lines |
| `/n` | Display line numbers |
| `/i` | Ignore case sensitivity |
| `/off[line]` | Do not skip files with offline attributes |

---

# 9. Copying Files

## 9.1 COPY — Copy Files

The `copy` command copies one or more files from one location to another.

Syntax:

```cmd
copy source destination
```

Example:

```cmd
copy notes.txt backup.txt
```

Copy a file into another directory:

```cmd
copy notes.txt Documents\
```

Copy a file using absolute paths:

```cmd
copy "C:\Users\Varun\notes.txt" "D:\Backup\"
```

Copy multiple files of the same extension:

```cmd
copy *.txt D:\Backup\
```

Copy all files from one directory:

```cmd
copy *.* D:\Backup\
```

### Important COPY Operators

| Symbol | Description |
|---|---|
| `*` | Represents multiple characters |
| `?` | Represents a single character |

Examples:

```cmd
copy *.jpg D:\Images\
copy report?.txt D:\Reports\
```

**Note:** If the destination file already exists, CMD may ask whether to overwrite it. The `/y` option suppresses that confirmation, so use it carefully.

---

# 10. Copying Directories

The `copy` command is designed for files. For directory trees, use `xcopy` or `robocopy`.

## 10.1 XCOPY — Copy Files and Directory Trees

The `xcopy` command copies files and directories, including their subdirectories.

Syntax:

```cmd
xcopy source destination [options]
```

Copy a directory and its contents:

```cmd
xcopy Projects Backup\Projects /E
```

Copy all files and subdirectories, including empty directories:

```cmd
xcopy Projects Backup\Projects /E /I
```

Copy hidden and system files too:

```cmd
xcopy Projects Backup\Projects /E /H
```

Preserve file attributes:

```cmd
xcopy Projects Backup\Projects /E /K
```

### Important XCOPY Options

| Option | Description |
|---|---|
| `/S` | Copy directories and subdirectories, excluding empty ones |
| `/E` | Copy directories and subdirectories, including empty ones |
| `/H` | Copy hidden and system files |
| `/I` | Assume destination is a directory when ambiguous |
| `/Y` | Suppress overwrite confirmation |
| `/K` | Preserve file attributes |
| `/D` | Copy files changed on or after a specified date |
| `/C` | Continue copying even if errors occur |
| `/V` | Verify each new file |

**Note:** `xcopy` is an older utility. For more advanced directory copying, Microsoft recommends considering `robocopy`.

## 10.2 ROBOCOPY — Robust File Copy

`robocopy` is a powerful Windows command-line utility for copying directories and their contents.

Syntax:

```cmd
robocopy source destination [file] [options]
```

Copy a directory:

```cmd
robocopy Projects Backup\Projects
```

Copy all subdirectories, including empty ones:

```cmd
robocopy Projects Backup\Projects /E
```

Copy subdirectories but exclude empty ones:

```cmd
robocopy Projects Backup\Projects /S
```

Copy files and preserve directory structure:

```cmd
robocopy Projects Backup\Projects /E /COPY:DAT
```

### Important ROBOCOPY Options

| Option | Description |
|---|---|
| `/S` | Copy subdirectories, excluding empty ones |
| `/E` | Copy subdirectories, including empty ones |
| `/Z` | Copy files in restartable mode |
| `/R:n` | Number of retries after failed copies |
| `/W:n` | Wait time between retries in seconds |
| `/MT:n` | Use multiple threads |
| `/COPY:DAT` | Copy data, attributes, and timestamps |
| `/LOG:file` | Write output to a log file |
| `/L` | List what would be copied without actually copying |

Example with retry settings:

```cmd
robocopy Projects Backup\Projects /E /R:3 /W:5
```

This attempts up to three retries with a five-second wait between retries.

### Important ROBOCOPY Warning

Be careful with `/MIR`.

```cmd
robocopy Source Destination /MIR
```

`/MIR` mirrors the source directory to the destination. It can delete files from the destination that are not present in the source.

Do not use `/MIR` unless you understand its deletion behavior.

For a preview, use:

```cmd
robocopy Source Destination /MIR /L
```

---

# 11. Moving Files and Directories

## 11.1 MOVE — Move Files

The `move` command moves files from one location to another.

Syntax:

```cmd
move source destination
```

Move a file into another directory:

```cmd
move notes.txt Documents\
```

Move multiple text files:

```cmd
move *.txt Documents\
```

Move a file to another drive:

```cmd
move notes.txt D:\Backup\
```

## 11.2 Moving Directories

You can also move directories.

Example:

```cmd
move Projects Backup\
```

This moves the Projects directory into the Backup directory.

**Note:** The destination must be valid. If a directory or file with the same name already exists, CMD may ask how to proceed.

---

# 12. Renaming Files and Directories

## 12.1 REN — Rename Files

The `ren` command renames a file.

Syntax:

```cmd
ren old_name new_name
```

Example:

```cmd
ren notes.txt study-notes.txt
```

Rename a file using a wildcard:

```cmd
ren *.txt *.bak
```

Use wildcards carefully because they can affect multiple files.

## 12.2 Rename Directories

The same command can rename a directory.

Example:

```cmd
ren OldProjects NewProjects
```

**Important:** `ren` renames an item in its current location. It does not move the item to another directory.

---

# 13. Deleting Files

## 13.1 DEL — Delete Files

The `del` command deletes files.

Syntax:

```cmd
del filename
```

Example:

```cmd
del notes.txt
```

Delete multiple files:

```cmd
del *.tmp
```

Delete all text files in the current directory:

```cmd
del *.txt
```

Ask for confirmation before deleting each file:

```cmd
del /p *.txt
```

Delete files quietly without confirmation:

```cmd
del /q *.tmp
```

Delete matching files in the current directory and its subdirectories:

```cmd
del /s *.tmp
```

### Important DEL Options

| Option | Description |
|---|---|
| `/p` | Prompt before deleting each file |
| `/f` | Force deletion of read-only files |
| `/s` | Delete matching files from subdirectories |
| `/q` | Quiet mode; suppress confirmation prompts |
| `/a` | Select files by attributes |

**WARNING:** `del` does not normally move files to the Recycle Bin. Deleted files may be difficult or impossible to recover.

Avoid combining `/s`, `/q`, and broad wildcards unless you are absolutely certain about the target.

For example, never casually execute:

```cmd
del /s /q *.*
```

---

# 14. Viewing Directory Structure

## TREE — Display Folder Structure

The `tree` command displays the directory structure in a tree format.

Syntax:

```cmd
tree [path] [options]
```

Display the current directory structure:

```cmd
tree
```

Display the structure of another directory:

```cmd
tree C:\Users\Varun\Documents
```

Display filenames along with directories:

```cmd
tree /f
```

Display the structure using ASCII characters:

```cmd
tree /a
```

Combine options:

```cmd
tree /f /a
```

Save the directory structure to a text file:

```cmd
tree /f /a > structure.txt
```

Example output:

```text
C:.
+---Documents
|   +---Notes
|   |       chapter1.txt
|   |       chapter2.txt
|   |
|   +---Projects
|           website.html
|
+---Downloads
        setup.exe
```

---

# 15. Viewing and Changing File Attributes

Windows files have attributes that describe certain properties.

Common attributes include:

- Read-only
- Hidden
- System
- Archive

## 15.1 ATTRIB — Display File Attributes

The `attrib` command displays or changes file attributes.

Syntax:

```cmd
attrib [options] [filename]
```

Display attributes:

```cmd
attrib notes.txt
```

Display attributes of all files in the current directory:

```cmd
attrib
```

## 15.2 Changing Attributes

Add the read-only attribute:

```cmd
attrib +r notes.txt
```

Remove the read-only attribute:

```cmd
attrib -r notes.txt
```

Add the hidden attribute:

```cmd
attrib +h notes.txt
```

Remove the hidden attribute:

```cmd
attrib -h notes.txt
```

Add the system attribute:

```cmd
attrib +s notes.txt
```

Remove the system attribute:

```cmd
attrib -s notes.txt
```

### Important ATTRIB Options

| Option | Description |
|---|---|
| `+r` | Set read-only attribute |
| `-r` | Remove read-only attribute |
| `+h` | Set hidden attribute |
| `-h` | Remove hidden attribute |
| `+s` | Set system attribute |
| `-s` | Remove system attribute |
| `+a` | Set archive attribute |
| `-a` | Remove archive attribute |
| `/s` | Process matching files in subdirectories |
| `/d` | Process directories as well |

Example:

```cmd
attrib +h +r notes.txt
```

This marks the file as both hidden and read-only.

**Important:** Hiding a file is not a security mechanism. Hidden files can still be accessed if their location is known.

---

# 16. Comparing Files

## FC — File Compare

The `fc` command compares two files and displays their differences.

Syntax:

```cmd
fc [options] file1 file2
```

Compare two text files:

```cmd
fc file1.txt file2.txt
```

Compare files without considering uppercase and lowercase differences:

```cmd
fc /c file1.txt file2.txt
```

Compare files line by line:

```cmd
fc /l file1.txt file2.txt
```

Compare binary files:

```cmd
fc /b file1.bin file2.bin
```

### Important FC Options

| Option | Description |
|---|---|
| `/b` | Perform a binary comparison |
| `/c` | Ignore case differences |
| `/l` | Compare files as ASCII text |
| `/n` | Display line numbers |
| `/w` | Ignore whitespace differences |

---

# 17. Working with Wildcards

Wildcards allow commands to match multiple filenames.

CMD supports two commonly used wildcard characters.

## 17.1 Asterisk (*)

The asterisk represents zero or more characters.

Examples:

```cmd
dir *.txt
```

Displays files ending in `.txt`.

```cmd
dir report*
```

Displays files whose names begin with `report`.

```cmd
del *.tmp
```

Deletes matching `.tmp` files in the current directory.

## 17.2 Question Mark (?)

The question mark represents one character in a filename pattern.

Example:

```cmd
dir file?.txt
```

This matches names such as:

```text
file1.txt
file2.txt
fileA.txt
```

### Wildcard Reference

| Pattern | Meaning |
|---|---|
| `*.txt` | All files ending in `.txt` |
| `report*` | Names beginning with `report` |
| `file?.txt` | `file` followed by one character and `.txt` |
| `*.jpg` | All JPG files |
| `data*.*` | Files whose names begin with `data` |

**Safety:** Always use `dir` to inspect wildcard matches before using a destructive command such as `del`.

---

# 18. Understanding Command Redirection

Redirection controls where command input and output go.

## 18.1 Output Redirection (>)

The `>` operator sends output to a file.

Example:

```cmd
dir > files.txt
```

This saves the directory listing in `files.txt`.

If the destination file already exists, its contents are overwritten.

## 18.2 Append Redirection (>>)

The `>>` operator appends output to an existing file.

Example:

```cmd
dir >> files.txt
```

This adds the directory listing to the end of `files.txt`.

## 18.3 Input Redirection (<)

The `<` operator takes input from a file.

Example:

```cmd
sort < names.txt
```

This passes the contents of `names.txt` to the `sort` command.

## 18.4 Pipe Operator (|)

The pipe operator sends the output of one command to another command.

Example:

```cmd
dir | more
```

This displays the directory listing one screen at a time.

Another example:

```cmd
dir /b | find ".txt"
```

This filters the directory listing for entries containing `.txt`.

### Redirection Reference

| Operator | Meaning |
|---|---|
| `>` | Redirect output and overwrite destination |
| `>>` | Redirect output and append |
| `<` | Take input from a file |
| `|` | Pass output to another command |

---

# 19. Useful File and Directory Commands — Quick Reference

| Command | Purpose |
|---|---|
| `dir` | Display files and directories |
| `cd` | Change directory |
| `md` | Create directory |
| `mkdir` | Create directory |
| `rd` | Remove directory |
| `rmdir` | Remove directory |
| `copy` | Copy files |
| `xcopy` | Copy directory trees |
| `robocopy` | Robust directory copying |
| `move` | Move files and directories |
| `ren` | Rename files and directories |
| `del` | Delete files |
| `erase` | Delete files |
| `type` | Display text file contents |
| `more` | Display output page by page |
| `find` | Search for text |
| `tree` | Display directory structure |
| `attrib` | Display or change file attributes |
| `fc` | Compare files |

---

# 20. Important Differences Between Commands

## 20.1 COPY vs XCOPY vs ROBOCOPY

| Feature | COPY | XCOPY | ROBOCOPY |
|---|---|---|---|
| Copy individual files | Yes | Yes | Yes |
| Copy directories | No, not as a directory tree | Yes | Yes |
| Copy subdirectories | No | Yes | Yes |
| Include empty directories | No | Yes, with `/E` | Yes, with `/E` |
| Restartable mode | No | No | Yes |
| Advanced retry options | No | Limited | Yes |
| Suitable for large directory transfers | Limited | Older utility | Yes |

## 20.2 DEL vs RD

| Command | Purpose |
|---|---|
| `del` | Deletes files |
| `rd` | Removes directories |
| `rd /s` | Removes a directory and its contents |

## 20.3 REN vs MOVE

| Command | Purpose |
|---|---|
| `ren` | Changes the name of an item |
| `move` | Moves an item to another location |

## 20.4 MD vs COPY CON

| Command | Purpose |
|---|---|
| `md` | Creates a directory |
| `copy con` | Creates a file from keyboard input |

---

# 21. Common Errors and Troubleshooting

## Error 1: The system cannot find the path specified.

Possible causes:

- The directory does not exist.
- The path is incorrect.
- The drive letter is incorrect.
- A folder name containing spaces was not quoted.

Example:

Incorrect:

```cmd
cd C:\Users\Varun\My Documents
```

Correct:

```cmd
cd "C:\Users\Varun\My Documents"
```

## Error 2: Access is denied.

Possible causes:

- Insufficient permissions.
- The file is protected.
- Another application is using the file.
- The operation requires elevated privileges.

Possible solution:

Open CMD as Administrator only when the operation genuinely requires administrative access.

## Error 3: The directory is not empty.

This occurs when trying to remove a directory that contains files or subdirectories.

Example:

```cmd
rd Projects
```

If the directory contains data, this command will fail.

To remove the directory tree:

```cmd
rd /s Projects
```

Remember that this deletes its contents too.

## Error 4: File not found.

Possible causes:

- Incorrect filename.
- Incorrect extension.
- Wrong current directory.
- Typographical error.

Check the directory:

```cmd
dir
```

## Error 5: Destination already exists.

This can happen when copying, moving, or renaming files.

Check the destination before overwriting anything.

---

# 22. Important Safety Rules

1. Always verify the current directory before deleting files.
2. Use `cd` and `dir` to confirm the location.
3. Be careful with wildcards such as `*.*`.
4. Avoid `/s` and `/q` together unless you understand the full impact.
5. Do not use `rd /s` on important directories without checking their contents.
6. Do not use `robocopy /MIR` casually because it can delete destination files.
7. Do not assume that CMD deletions go to the Recycle Bin.
8. Use quotation marks around paths containing spaces.
9. Do not run commands from unknown sources without understanding them.
10. Use Administrator mode only when necessary.

---

# 23. Key Takeaways

After studying this lesson, you should understand:

- The difference between files and directories.
- Absolute and relative paths.
- How to navigate using `cd`.
- How to list files using `dir`.
- How to create directories using `md` and `mkdir`.
- How to remove directories using `rd` and `rmdir`.
- How to create and read text files.
- How to copy files using `copy`.
- How to copy directories using `xcopy` and `robocopy`.
- How to move and rename files.
- How to delete files.
- How to inspect directory structures using `tree`.
- How to manage attributes using `attrib`.
- How to compare files using `fc`.
- How to use wildcards and redirection.

---

# 24. Official Documentation

Use official Microsoft documentation as your primary reference.

- [Windows Commands Documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [DIR](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/dir)
- [CD](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cd)
- [MD](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/md)
- [RD](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/rd)
- [COPY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/copy)
- [XCOPY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/xcopy)
- [ROBOCOPY](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/robocopy)
- [MOVE](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/move)
- [REN](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ren)
- [DEL](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/del)
- [TREE](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tree)
- [ATTRIB](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/attrib)
- [FC](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/fc)

---

**End of Lesson 03 — File and Directory Management in Windows CMD**
