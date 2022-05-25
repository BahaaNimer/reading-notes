# What Is The Command Line

A command line, or terminal, is a text based interface to the system.

You are able to enter commands by typing them on the keyboard and feedback will be given to you similarly as text.

## Opening a Terminal

- If you're on a Mac then you'll find the program Terminal under Applications -> Utilities. An easy way to get to it is the key combination 'command + space' which will bring up Spotlight, then start typing Terminal and it will soon show up.

- If on Linux then you will probably find it in Applications -> System or Applications -> Utilities. Alternatively you may be able to 'right-click' on the desktop and there may be an option 'Open in terminal'.

- If you are on Windows and intend to remotely log into another machine then you will need an SSH client.

## The Shell

The most common one is called bash which stands for Bourne again shell.

> you may use a command called `echo` to display a system variable stating your current shell. `echo` is a command which is used to display messages.

To see where are you in the terminal :

pwd : Print Working Directory

```
pwd
```

To list the contents of my current directory :

```
ls / ls [options] [location]
```

## Absolute and Relative Paths

- absolute : specify a location (file or directory) in relation to the root directory.
- relative : specify a location (file or directory) in relation to where we currently are in the system.

typs of paths :

```
/ : refer to home directory or root directory
~/directory : from root enter the directory
./directory : from your current location enter the directory
../directory : exit from your current location then enter the directory
```

To move around :

cd : Change Directories

```
cd [location]/[path] : go to
cd .. : go back
```

> you can enter TAP to an auto complete action.

To know the file type you can use :

```
file [path]
```

> Linux is Case Sensitive so be careful :)

> Also don't use spaces in names

> You can use single or double quotes

Escape Characters :

```
\ : to escape (or nullify) the special meaning of the next character.
```

To hidden a file or directory :

> you need to put " . " before the name.

To see the hidden files or directorys :

```
ls -a
```

## The manual pages

The manual pages are a set of pages that explain every command available on your system including what they do, the specifics of how you run them and what command line arguments they accept.

```
man <command to look up>
```

## For Searching

```
man -k <search term>
```

> Press q to exit man pages

## Making a Directory

```
mkdir [options] <Directory>
 -p : which tells mkdir to make parent directories.
 -v : which makes mkdir tell us what it is doing.
```

## Removing a Directory

```
rmdir [options] <Directory>
```

## Creating a Blank File

```
touch [options] <filename>
```

## Copying a File or Directory

```
cp [options] <source> <destination>
```

## Moving a File or Directory

```
mv [options] <source> <destination>
```

## Removing a File (and non empty Directories)

```
rm [options] <file>
rm -rf <file> : for non empty directories
```
