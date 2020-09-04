# Session 1:  Shell for Navigating to and Working with Files and Directories


## Challenge Questions
1. Does type case matter?  Is there a difference between `ls -s` and `ls -S`?

2. Do spaces matter?  Is there a difference between `ls-F` and `ls -F`?

**Explore more `ls` flags.**  

5. The default `ls` lists contents in alphabetical order.  What option do I use to see them by time of last change?

6. Moving files.  We accidentally put the files `sucrose.dat` and `maltose.dat` into the wrong folder, `analyzed/`.  Fill in the blanks to move these files into the `raw/` folder.
```
$ ls -F
  analyzed/  raw/
$ ls -F analyzed/
  fructose.dat glucose.dat maltose.dat sucrose.dat
$ cd analyzed
```
My next line of code should be (fill in the blanks):
```
$ mv sucrose.dat matose.dat ___/___
```
<details>
  <summary>Solution</summary>
  Think about ../raw
  Recall that .. refers to the parent directory (i.e. one above the current directory).
</details>

7. Renaming Files. We mispelled a filename!  Which of the following commands will correct our mistake?
    - a. `cp statstics.txt statistics.txt`
    - b. `mv statstics.txt statistics.txt`
    - c. `mv statistics.txt . `
    - d. `cp statstics.txt .`

<details>
  <summary>Solution</summary>
  <p>(a.) Will copy the file, so we will end up with the mispelled and correct version.
  (b.) Will move (i.e. rename) the incorrect file name to a correct filename.
    (c.) and (d.) will not work. Remember . is the current directory.</p>
</details>

8. Removal. What happens when we execute `rm -i thesis/finaldraft.txt`? Why would we want this protection when using `rm`?
<details>
  <summary>Solution</summary>
  The program will confirm that we want to delete the thesis final draft file.  Remember, deletion is forever!  There is no trash can or recycle bin.
</details>

9. Removal. What is wrong with the command `rm -i thesis`?
<details>
  <summary>Solution</summary>
  The remove command will not act on a directory unless the recursive option (-r)is given. 
</details>

10. Removal. What is wrong with the command `rm -r thesis`?
<details>
  <summary>Solution</summary>
  This remove command will delete the directory thesis and all its contents, but we forgot to check for confirmation with the interaction option (-i).  Remember, deletion is permanent!
</details>

11. Wildcards.  Which of the following matches the file names `ethane.dat` and `methane.dat`?
   - a. `ls ?ethane.dat`
   - b. `ls *ethane.dat`
   - c. `ls ???ane.dat`
   - d. `ls ethane.*`
<details>
  <summary>Hint</summary>
  Remember ? wildcard matches to exactly one character.  * wildcard can match to zero to many characters.
</details>

 

## Questions of the day:
- What is a command shell and why should I use one?
- How can I move around on my computer?
- How can I see what files and directories I have?
- How can I specify the location of a file or directory on my computer?
- How can I create, copy, and delete files and directories?
- How can I edit files?

## What is Unix Shell?
- _It is different from how we usually interact with our devices, on a **graphical user interface** (GUI)_
- Shell is a **Command-Line Interface** (CLI) 
  - Type commands in the **prompt** `$`
  - Invoke complicated programs
- Shell is a scripting language
- We will use the Unix Shell: Bash (Bourne Again SHell by Stephen Bourne)

## Why use Bash?
- Combine existing tools into powerful pipelines and handle large volumes of data automatically. 
- Sequences of commands can be written into a script, improving the reproducibility of workflows.
- Essential to interface with hardware, HPCC, and remote machines.
- Commands and the grammar of shell are used in other coding languages.

## How do I navigate files and directories?
- **File System**: The part of the operating system responsible for managing files and directories
  - **Files** hold information
  - **Directories** (or **folders**) hhold files or other directories.  Thinks of them like _places_.
- **Current working directory** is the place where you are in the file system when you are using the shell.
- **Root directory** is the top directory that holds everything else.  It is refered to by a slash `/` on its own.  This is the leading slash in other directory paths, for example `/Users/claire/`
- **Hidden files and directories** start with `.` like `.bash_profile`.  They are usually configuration settings and are hidden to prevent cluttering the terminal with a standard `ls` command.  Add the `-a` option see hidden files. 

## What is the general syntax of a shell command?
**Bash**
```
$ ls -F /
```
`ls` is the **command**, with an **option** (or **switch** or **flag**) `-F` and an **argument** `/`.
**Options** start with a single dash (`-`) or two dashes (`--`) and change the behavior of the command.
Arguments tell the command what to operate on (e.g. files and directories).
Options and argements are refered to as **parameters**.

_Type case is important._
_Spaces are important between command and options. (But options can be combined with a single - and no spaces)_




## Tips for good names for files and directories
1. Don't use spaces.  Use `-` or `_` or _camelCase_.
1. Don't begin a name with a `-` (dash).  It will look like a command option.  Names should start with letters or numbers.
1. Avoid special characters.  Some have special meanings.

_If you need to refer to names of files or directories that have spaces, put them in quotes ("")._


### What's in a name?
A **filename extension** is the second part of the filename after the dot (.).  They help us and programs tell different kinds of files apart.  A few examples:
 - .txt: plain text file
 - .csv: comma separated value file
 - .pdf: PDF document
 - .cfg: configuration file of parameters for a program
 - .png: an image file

The **wildcard** `*` matches zero or more characters.  For example, to access all the text files in a directory, use `*.txt`.

The **wildcard** `?` matches exactly one character. 



## Which editor should I use?
- `nano` is a built-in text editor that only works with plain character data (i.e. no tables, images, or other media).  It is the least complex, but you may want to try more powerful editors.

**For Unix Systems (Linux and macOS)** 
- [Emacs](http://www.gnu.org/software/emacs)
- [Vim](http://vim.org/)
- [Gedit](http://projects.gnome.org/gedit/) is a graphical editor

**For Windows**
- [Notepad++](http://notepad-plus-plus.org/)
- `notepad` is built-in and can be run in the command line

_If you start an editor from the shell, it will use your current working directory as its default location._

_In editor commands, the Control key is also called Ctrl or ^._


### Getting help
- The help option can be used with a command, for example `ls --help`
- The manual (`man`) for a command can be accessed, for example `man ls`



## Commands of the day: Navigating
- `ls`: listing.  This command will list the contents of the current directory
  - `-F` option (switch or flag) tells ls to classify the output by adding a marker to file and directory names to indicate what they are.
  - `-s` option displays the size of files and directories
  - `-S` option will sort the files and directories by size
  - `--help` option will tell us how to use the command and what options it accepts
- `pwd`: print working directory.  Directories are like places, at any time while we are using shell, we are in one place, called our current working directory
- `clear`:  clears the terminal if it gets to cluttered
- up and down arrows can be used to access previous commands (or scroll)
- `man` will give you the manual for a command, for example `man ls` will tell us all about listing
- `cd` will change your working directory.  `cd` can only see sub-directories inside your current working directory.
  - `cd ..` is a shortcut to move up one directory to the _parent directory_ of the one we are in
  - `cd ~/` is a shortcut to move to the current user's home directory.  For example, if my home directory is `/Users/claire`, then `~/data` is equivalent to `Users/claire/data'

## Commands of the Day: Creating, Moving, and Deleting
- Creating Directories or Files:
  - `mkdir path` creates a new directory
  - `nano new` runs a text editor called Nano to create a new file by the new name given.  For example, `nano thesis.txt` creates a text file named `thesis.txt` in the working directory. 
  - `touch new` creates an empty (0 byte) file by the new name given. Why bother? Some programs require empty files to populate with output.
- Moving or Renaming directories or files safely:
  - `mv old new` command move has two arguments.  The first tells `mv` what we're moving, while the second is where it's to go.
  - `mv -i` or `mv -interactive` must be used to make `mv` ask for confirmation before overwriting any existing file or directory with the same name as the second argument. (Otherwise, Beware! It will silently overwrite.)
- Copying directories and/or files:  
  - `cp old new` command copies a file (first argument) to a new location (second argument)
  - `cp -r` adds the recursive option to copy a directory and all its contents to another directory (second argument).  For example, we can make a backup with `cp -r thesis thesis_backup`.
  - `cp` can be used on multiple filenames as long as a destination directory is the last argument. For example, `cp a.txt b.txt c.txt backup/` will copy the three text files into the subdirectory `backup/`.
- Removing files and directories safely: **Deleting is forever**
  - `rm -i path` command for remove with interactive option to ask for confirmation before deleting.
  - `rm -i -r path` command with interactive option and recursive option will **remove a directory and all its contents** with confirmation prompts.    
  

  



## Challenge Project for Next Time (optional)
Before heading on a trip, you want to back up your data and send some datasets to Claire.  Fill in the following commands to get the job done.  First, let's set up a directory and files.

``` 

# Change to your desktop 

# Make a new folder for our fake data and go into it

# Create some empty files.

# Make sure the new files are created.

# Let's add some info to our file and confirm it with the editor

# Let's edit and add information to another.

```

When you're ready, see a possible solution at [example solution](session-1-solution.md).


### References
- [Intermediate Linux Commands](https://docs.google.com/document/d/1xY7fSNBzChx5PMPF_tGoBWOwXef5wVsH1Mf7vLdgJz0/edit?usp=sharing)
- [Software Carpentry Unix Shell](http://swcarpentry.github.io/shell-novice/)




