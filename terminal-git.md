# Terminal

- **Terminal** is the command line interface (CLI):
  - Expected output/last login
  - Prompt: provides context about `cwd`
  - Command line
  -	**Nano** is a terminal text editor that provides easy-to-read instructions and is available on most systems
	  - Preferable to VSCode in instances where you need to log into a remote server to edit or configure files

#### Terminal Shortcuts:
| Command      | Action                                |
|--------------|---------------------------------------|
| Return/Enter | submit command                        |
| Tab          | Autofill file/directory name          |
| Ctrl + A     | move cursor to beginning of line      |
| Ctrl + E     | move cursor to end of line            |
| Ctrl +U      | clear line before cursor              |
| Ctrl + K     | clear line after cursor               |
| Ctrl + L     | clear terminal screen (Joe’s pro-tip) |
| Ctrl + C     | kill what’s running                   |
| Ctrl + R     | search previous commands              |
| Ctrl + _     | undo last command                     |

### Navigationg your File System

#### Change Directory:
|  Command      |  Action                   |
|---------------|---------------------------|
| `/`           |   top level directory     |
| `.`           |   current directory       |
| `.. `         |   parent directory        |
| `~`           |   home directory          |
| `cd`          |   home directory          |
| `cd – `       |   previous directory      |
| `pwd `        |  print working directory |
| `cd../..`     |   move up two levels      |

#### File & Directory Management:
| Command    |   Action                                             |
|------------|------------------------------------------------------|
| `mkdir`      |    create new folder                                 |
| `rmdir`      |    delete empty folder                               |
| `-r`         |     delete folder and its contents                   |
| `rm`         |    delete a file                                     |
| `touch`      |    create new file                                   |
| `cp`         |    copy file                                         |
| `mv`         |    move/rename file or folder                        |
| `ls`         |    list files and subdirectories                     |
| `curl`       |    download URL Contents to local file               |
| `curl -o`    |    download URL Contents to local file and name file |

#### `grep`
- `grep` (g/re/p: **G**lobally search for a **R**egular **E**xpression and **P**rint)
  - Finds text in file(s)
  - Accepts two arguments:
    - **Pattern**: search value
    - **Source**: file to search
  - Example: Search file.txt for phrase "hello":
    `grep "hello" file.txt`

<u>Options</u> alter behavior of command line instructions and can be set with:

#### Shorthand Commands
| Command  |  Action                              |
|----------|--------------------------------------|
| `-a`        |     all files                        |
| `-l`        |     list format                      |
| `-la`       |     list all files                   |
| `-p`        |     parent directory                 |
| `-r`        |     recursive                        |
| `-n`        |     line number                      |
| `-c`        |     count                            |
| `-s`        |     sort entries by size             |
| `-i`        |     warn before execution            |
| `-f`        |     force without warning            |
| `-lt`       |     sort entries by time modified    |
| `-lh`       |     display files sizes (KB, MB, GB) |
| `-lo`       |     display size, owner, & flags     |    
---
## The Shell
-	Software layer that translates CLI into actual commands
-	Uses input to call applications
-	Supports user environments/customization
-	Operating system translates CLI to machine code to be processed by CPU

#### Shell Scripting
-	Granting a test file permission to execute
-	Create new script file with `.sh` extension
-	Initialize shell script with #!(shebang) followed by application path:
`#!/bin/zsh`

#### Shell Permissions
- File permissions are represented by ten characters on command line:
<img src="https://appacademy-open-assets.s3-us-west-1.amazonaws.com/Module-Unix/cli/assets/cli-unix-permissions.png" />

-	The first character is the directory indicator
	 - `d`: directory
	 - `i`: file
-	The directory indicator is followed by three permission groups:
    - `u`: user/owner
    - `g`: group
    - `o`: others
-	Each group has three permissions (in order):
	  - `r`: (read) view a file or directory’s content
    - `w`: (write) modify a file or directory’s content
    - `x`: (execute) navigate into directory and run file
-	**Numeric permission** notation: (seen in documentation and error messages)
	  - `r` = 4
	  - `w` = 2
	  - `x` = 1
     Example:
     `-rw-r--r-- = 644`
-	Modifying permissions
  - `chmod` (change mode) command updates a files’ permissions
	  - Grant or revoke permission with `+` or  `–` following group type (u, g, o)and preceding permission type (`r, w, x`)
`+` : grant permission
`-`	: revoke permission
-	if permission group is not specified—all groups will be modified
    - Example: Grant (+) permission to the group (g) to read (r) a text file:
`chmod  g + r  file.txt`


#### Start-Up Files
- `Bash`: Default shell for Linux systems; uses login and non-login shells
	 - **Login shell** : `.bash_profile` is executed when bash is started manually with `-l` or `–login`
	   - If no `.bash_profile`, bash will run `.profile`
	 - **Non(auto)-login shell**: executes `.bashrc` automatically

- `Zsh`: Default shell for MacOS; only uses non(auto)-login when `zsh` is started
	 - Executes .zshrc file


---
# Git
-	Git is a Version Control System (VCS) that helps us track changes to our projects over time
    -	Git is the most popular VCS in use today
-	The **repository** comprises all the source code for a particular project
-	**Commits** are a collection of changes grouped towards a shared purpose.
-	A **hash** is specially generated series of letters and number that identifies each commit in addition to a detailed message describing the changes
-	They are 40 characters long, but Git abbreviates to seven characters
-	The head is a default reference of the most recent commit
-	Git maintains three lists of changes:
    -	**Working Directory**: in-progress changes
    -	**Staging Area**: changes ready to be committed
    -	**Commit History**: changes already committed
-	**Branches** are separate timelines in Git, reserved for it’s own changes/commits
    -	**Master branch** is the default branch
-	*Golden rule of Git*: **Never modify shared branches**

#### Git Commands
|Commands    | Actions                                                                                                   |
|------------|------------------------------------------------------------------------------------------------------------|
| `git config` |                                      Configure author name and email to be associated with commits         |
| `git init`   |                                           Converts a local directory into a Git repository                 |
| `git status` |                                      Lists modified files and changes that need to be added or committed   |
| `git add`    |                                    Add everything within the directory to the repo                         |
| `<file><file>` |               Add specific files to the repo                                                              |
| `*.txt`        |                              Add all text files to the repo                                              |
| `git commit`   |                                    Snapshot of all the files in the repository (with changes)            |
| `-m “<message>”` |              Label commit with message detailing changes                                               |
| `--amend`        |                       Alter the latest commit                                                          |
| `^`              |                                                       Move upwards one commit (per ^)                  |
| `git diff`       |                                View changes in the working directory                                   |
| `--staged`       |                     View changes in Staging Area                                                       |
| `<branch>`       |                         View changes in specific commit                                                |
| `<branch>^!`     |                      View changes between specific commit and commit before it                         |
| `<branch><branch>`|          View changes between two specific commits                                                    |
| `git log`         |                                        View commit ID                                                 |
| `git branch`      |                                 View all branches in repository                                       |
| `-f <branch>`     |                   Directly reassign a branch to a commit                                              |
| `-d <branch>`     |                   Delete branch                                                                       |
| `git checkout <branch>` |         Switch from branch to another                                                           |
|` -b <branch>`           |             Create a new branch and switch to it                                                |
| `git merge <branch>`     |              Merge a branch into your active branch                                            |
| `git clone /path/to/repository` | Creates working copy of local repository                                                 |
| `git grep “variable”`         |            Search working directory for “variable”                                        |
| `git reset`                    |                       Reverse changes of commit to previous commit                       |
| `git revert`                  |                     Reverse changes of commit and share those changes with others         |
| `git clone`                   |                        Create local copies of remote repositories                         |
| `git fetch`                   |                        Downloads commits in remote repository that are missing from local |
