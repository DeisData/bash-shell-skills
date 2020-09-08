# Session 2: Pipes, Filters, and Loops
The idea of linking together programs is why Unix has been so successful.
Instead of creating enormous programs that try to do many  different things, we focus on lots of simple tools that work well with each other.
We improve productivity through automation -- with loops!

### Challenge Questions:
1. In our current directory, we want to find the three files which have the least number of lines.  Which command listed below would work?
 - a.  `$  wc -l * > sort -n > head -n 3`
 - b.  `$  wc -l * | sort -n | head -n 1-3`
 - c.  `$ wc -l * | head -n 3 | sort -n`
 - d.  `$ wc -l * | sort -n | head -n 3`
 
2. See the file called `data-shell/data/animals.txt.` 
What text passes through each of the pipes and the final redirect in the pipeline below?

`$ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt`

Hint:  Build the pipeline up one command at a time to test your understanding.
 
3.  `uniq` filters out adjecent matching lines in a file.  
How can we extend the pipeline to find out what animals the file `data-shell/data/animals.txt` contains without any duplicates?
<details>
<summary>Solution</summary>
cut -d , -f 2 animals.txt | sort | uniq > animals_unique.txt
</details>

4. Assuming your current working directory is `data-shell/data/`, which command would you use to produce a table that shows the total count of each type of animal in the file `animals.txt`?
  - a. `$ sort animals.txt | uniq -c`
  - b. `$ sort -t, -k2, 2 animals.txt | uniq -c`
  - c. `$ cut -d, -f 2 animals.txt | uniq -c`
  - d. `$ cut -d, -f 2 animals.txt | sort | uniq -c`
  - e. `$ cut -d, -f 2 animals.txt | sort | uniq -c | wc -l`

5. Nested Loops Challenge!  What does this do?

```
$ for species in cubane ethane methane
> do
>     for temperature in 25 30 37 40
>     do
>         mkdir $species-$temperature
>     done
> done
```

## Questions of the day:
- How can I combine existing commands to do new things?
- How can I write to a file from the shell prompt?
- How can I perform the same actions on many different files?

     
## Commands of the Day
- **Filters** are programs that transform a stream of input into a stream of output
  - `wc` is the word count command for number of lines, words, and characters in a file (left to right in that order)
  - `echo` prints a string or the value of a variable as output.  For example 'echo The echo commmand prints text` or `echo $SHELL` prints the value of the variable `$SHELL` (a defined path)
  - `sort` sorts the contents of a file.  `sort -n ` sorts a numerical file.
- To escape a mistake in the prompt, type [Control] + [C] 
- Write to a file from the prompt
  - `>` **redirects** a command's output to a file instead of printing it to the screen.  DO NOT write to the same file.
  - `>>` **redirects* a command's output to append to the end of a file 
- View particular file contents
  - `cat`is the concatentate (join together) command that prints the contents of files one after another
  - `less` displays a screenful of the file and then stops.  You can go forward one screenful by pressingthe spacebar, or back one by pressing [b] and [q] to quit.
  - `head` shows the first few lines of a file.  For example, `head -n 5` will show the first 5 lines.
  - `tail` shows the last few lines of a file
  - `cut` removes or cuts out certain sections of each line in a file
     - `-d` option specifies a delimeter 
     - `-f` option specifies the column for extraction
  - `uniq` filters out adjecent matching lines in a file.
- Piping Commands Together
  - `|` command **pipe** tells the shell to use the output of a command on the left as the input of the command on the right
  - Chain pipes consecutively

**Loop Structure**
```{Loop Structure}
for thing in list_of_things
do
   operation_using $thing
done
```

## Loop Examples

### List the contents of working directory one item at a time
```
for itemname in *
do
   ls $itemname
done
```

### Output part of files in a directory
```
cd Desktop/data-shell/creatures
for filename in basilisk.dat minotaur.dat unicorn.dat
do 
   head -n 2 $filename
done
```

### Write files in a directory to a new file
```
cd Desktop/data-shell/creatures
for filename in basilisk.dat minotaur.dat unicorn.dat
do 
   cat -n 2 $filename >> all.pdb
done
```

### Repeat running a program with all your input data files
Nell has files NENE00000A.txt and NENE00000B.txt that need needs to run through th program
`goostats` one at a time.  The program `goostats` has two arguments, the input data file, and the output statistics file.

```
cd ../north-pacific-gyre/2012-07-03
for datafile in NENE*[AB].txt
do
    echo $datafile
    bash goostats $datafile stats-$datafile   #where stats-$datafile is the output of goostats program.
done
```

### Checking on your loop before you run it!
It can be a good idea to run your loop with `echo` in front of you commands, to make sure it will act the way you believe.  For example, in the loop above I may want to first run `echo "bash goostats $datafile stats-$datafile"` before I run the loop to execute the `goostats` program.  

## Commands We Already Know
- Navigating File System
  - `ls`: listing contents of working directory with many options: `-F` classify, `-a` list all, `-s` size, `-S` sort by size
  - `pwd` print working directory
  - `clear` the terminal
  - `man` will give you the manual for a command
  - `cd` will change working directory
  - `cd ..` change up to parent directory
  - `cd ~` change to home directory
- Creating Directories or Files:
  - `mkdir path` creates a new directory
  - `nano new` runs a text editor 
  - `touch new` creates an empty (0 byte) file
- Moving or Renaming directories or files safely:
  - `mv -i old new` 
- Copying directories and/or files:  
  - `cp old new` 
  - `cp -r` to copy a directory and all contents
- Removing / Deleting Safely: **Deleting is forever**
  - `rm -i path` delete file with confirmation
  - `rm -i -r path` delete directory and contents    
- Wildcards
  - `?` matches to one character
  - `*` matches to zero to many characters
- Filters 
  - `wc` is the word count 
  - `echo` prints text or the value of a variable
  - `sort` sorts the contents of a file.  `sort -n ` sorts numerically.
- Write to a file from Prompt
  - `>` **redirects** a command's output to a file 
  - `>>` **redirects* a command's output to append to end of a file 
- View particular file contents
  - `cat`concatentate prints the contents of files
  - `less` displays a screenful of the file and then stops
  - `head` shows the first few lines of a file
  - `tail` shows the last few lines of a file
  - `cut` removes or cuts out certain sections of each line in a file
     - `-d` option specifies a delimeter 
     - `-f` option specifies the column for extraction
  - `uniq` filters out adjecent matching lines in a file.
- Piping Commands Together
  - `|` command **pipe** tells the shell to use the output of a command on the left as the input of the command on the right
  


### Resources
This lesson is adapted from [The Unix Shell on Software Carpentry](http://swcarpentry.github.io/shell-novice/).


