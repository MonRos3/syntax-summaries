# Terminal Commands

Note: I use a Mac, so these terminal commands will differ from Windows-based systems. MacOS command-line interfaces [CLIs] uses a Unix-based shell, with some older systems using bash by default, and Mac systems [since Catalina] using zsh by default.

Later on I will make a file titled "Command Prompt" tailored for Windows CLI commands.

Some of these commands will work in PowerShell, but there may be some remaining differences due to PowerShell's unique syntax and command structure.

Linux users will be able to use these commands.

## Getting Oriented

Present working directory; print the path to where you currently are:

```bash
pwd   
```

List items [default setting: list items in current directory]:

```bash
ls 
```

List items; including hidden items [items with a “.” at the start of their name]:

```bash
ls -a    
```

```bash
whoami    //displays current username
```

Bonus:
<tab>       //auto-complete shortcut

```bash
clear    //clears the code line interface [CLI]
```

## Creating, Editing, Deleting Folder and Files

Change directory into a folder [how you move around in terminal]:

```bash
cd folder-name
```

Move up a folder:

```bash
cd ..    
```

Jump to home directory:

```bash
cd ~    
```

Create a new directory:

```bash
mkdir new-folder-name
```

Open a folder:

```bash
open folder-name
```

Create a file:

```bash
touch filename.extension
```

Edit a file:

```bash
nano filename.extension
```

Remove a file or folder:

```bash
rm file-or-folder-name
```

Recursively and forcibly remove the folder and its contents:

```bash
rm -rf folder-name
```

## Setting Up a Virtual Environment

Initialize a virtual environment:

```bash
virtualenv .venv
```

Activate the venv:

```bash
source .venv/bin/activate
```

Deactivate the venv:

```bash
deactivate
```

## Zip a File

tar -czf ~/path/zippedfile.zip ~/path-to-dest/folder

## Unzip a File

tar -x ~/path/somefile.zip

## Getting Help

man [command] //manual, type <q> to quit

[command] --help

[command] -h

## Misc

Display [string], passed as argument:

```bash
echo [option] [string]
```

Change password for a user:

```bash
passwd username
```

Linux can use script command, capture and replay terminal sessions.

```bash
script
```

Press <enter>

ctrl + d to exit
