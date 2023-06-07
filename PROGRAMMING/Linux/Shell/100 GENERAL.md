# Actions

Explanation file structure
```shell
drwxrwxrwx 3 user user-groups  4096 Jan 31 14:40  Music

  -    rw-   rw-  rw- 3 user user-groups  4096 Jan 31 14:40  Music
type    1    2     3
	  positions
	 1: user permissions
	 2: Group permissions
	 3: Other groups permissions

3              # Number of times the file is duplicated with command link(ln)
user           # user
user-groups    # user group
4096           # File size
Jan 31 14:40   # Modification date  
Music          # Dir name
```
```shell
drwxrwxrwx 3 user user-groups  4096 Jan 31 14:40  Music-> other

other # That indicate when we have created a symbolic link
```

### Permission Signals
| TYPE | (-) REGULAR FILE     | (d) DIRECTORY     |
|:----:| -------------------- |:----------------- |
| (-)  | No permissions       | No permissions    |
|  r   | read permission      | List permission   |
|  W   | Write permission     | Modify permission |
|  x   | Execution permission | Access permission |

```shell
history # Display all command history
```
```shell
Ctrl + R # Search commands

user@pc_name:/mnt/c/Users/user$ !50 #Execute the command numer 50 in the history
```

### General commands
```shell
apt-get install program # install package

apt-get remove program # uninstall package

apt-get purge program # uninstall package and delete all files

apt-cache search "package"
```

```shell
aptitude search "program" # Search program residues
```

```shell
pwd # Show the actuall path
```

```shell
man command # Displays a description and the options that this command allows
```

```shell
whoami # current user
```

```shell
group # User group
```

```shell
id # General info
```

```shell
tree # Show tree info
```

```shell
tr # Replace characters
tr a-z # Replace in range
tr [a*3] # Multiply strings
tr [:class:] # Replace one class
tr -d character # Delete indicate character
tr -s character # Delete character duplicates
tr -c character # All but the indicated characters. Invest
```

[[FIND|Find]]
```shell
find path options # Search for something
```

[List](LIST.md)
```shell
ls #List all folders and files on the current dir
```

[Create](CREATE.md)
```shell
mkdir # Create a folder
```

Insert
```shell
echo "message" >> file
echo -e "Hello \n World" # Escape to the special characters
echo "path==> $PATH" # Asign $PATH to path==> ("set variables")
echo 'path==> $PATH' # Print path==> $PATH ('Literal print')
```

[[EDIT#Copy|Copy]] 
_Change the user who created the file
```shell
cp  # Copy the file into a directory
```

[[EDIT#Move|Move]] 
_Does not change the user who created the file 

```shell
mv file_name dir # Move the file into a directory
```

Delete
```shell
rm -r # Delete a folder
```
```shell
rm # Delete a file
```

Show txt in the console
```shell
cat file_name # Display on the console what the file contains
more filename # Display on the console what the file contains but page a page
less filename # Display on the console what the file contains but page a page
head -n(optional) filename # Display ten first lines on the console what the file
tail filename # Display ten last lines on the console what the file
```

Filter Text
```shell
cut file_name # Select and show characters inside a file
cut -cn-x*n file_name # Select a range
cut -cn,x*n file_name # Select the character n and x*n
cut -d":" file_name # Select the character delimitator
cut -f file_name # Select the columns to shown

grep   # Shows only the lines that have any pattern
grep  -v # Don't Shows the lines that have the pattern
grep  -l # Which file has the lines that match the pattern
grep  -w # The pattern has to be a independent word
grep  -n # Indicate the line number
grep  -i # Doesn't matter uppercase or lowercase
grep  -c # It shows the total lines if it meet the pattern
grep  -r # Search files recursively
```


Commands on disc use:
```shell
df # Shows information about the system partitions, total size, used, free...
```
```shell
du # Shows information about the disk use
```

Links
```shell
ln # Creates a link to one file system element and that link is hard, When is created a file with this command, if we try to moddify it, all copies will also be modified. When we delete one copy, the other copies work the same as before, even without losing the data. Don´t create extra size on the disk
```
```shell
ln -s # creates a link to a file system item and that link is soft, similar to a shortcut, to directories will always make symlinks.
```

Wildcards
```shell
* # Indicate all coincidens e.g. ls -l us*=> search all coincidens that start with us
*.* # All files with extensions, not directories
*am* # All files that contains am
```
```shell
? # Replace a caracter
*inf?rm* # All files wich contains that structure name
```
