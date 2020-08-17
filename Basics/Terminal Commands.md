## Terminal Commands (Mac)

#### Navigation: 
- `cd {/path/to/folder}`: changes directory to specified path
- `cd /`: goes to root directory
- `cd ~`: goes to user directory
- `ls`: lists all files/folders in the current working directory
- `pwd`: prints the path to the current working directory|


#### Creating & Deleting:
- `mkdir {foldername}`: makes a folder with the specified nam
- `rm {filename}`: removes the specified file
- `rm -r {foldername}`: removes the specified folder recursively
- `touch {filename}`: creates the specified file|
- `mv {filename} {new filename}`: renames the file/folder to the 2nd name

#### Opening Files/Folders:
- `open {filename}`: opens the file with the default program
- `open {filename} -a "{program name}"`: opens the file in the specified application
- `open .`:  opens the current folder in finder
- `open . -a "{program name}"` opens the folder in the specified application

### Terminal Commands Different in Windows:
- dir - list files
- echo > {filename} - create an empty file
- del {filename} - remove a file
- rmdir {directory name} - remove a directory and all files within
- rename {filename} {new filename} - rename a file or folder
- start {filename} - open file in default program
- start . - open current directory
- cls - clear the terminal screen

## Vim Commands

|Command    | Function     |
|------- |-----------|
|i|insert/typing mode|
|esc|leave insert mode|
|:w|save additions|
|:wq|save & quit|
|:q!|quit & discard changes|


|Key|Movement|
|--|:--|
|w|front of next word|
|b|front of previous word|
|0|start of line|
|$|end of line|
|g|last line|
|a|append to final line|