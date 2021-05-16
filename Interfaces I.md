Interfaces I

The word asynchronous means "not happening at the same time" (lack of synchronisation). Asynchronous communication means that (significant) time elapses between transmission and reception.

Exercise: Give two examples of asynchronous communication. Give two examples of synchronous communication.

Reading command specifications

There is a special syntax for describing how to run a command: things enclosed in [square brackets] are optional. An ascii ellipsis "..." means "repeat".

Example: the cat program takes zero or more values for OPTION and zero or more values for FILE. (The possible values for OPTION and FILE are described in the help output.)

cat [OPTION]... [FILE]...
"Options" are small features which adjust how the program performs its job.

Exercise: Compare the output of ls vs ls -l and ls -a; describe how they are similar, and how they are different.

Some options take values: compare seq 5 vs seq -s , 5

Some options have long and short names: seq --separator=, 5

Navigating with the command-line

Read the following sections from Using the Command Line of Linux Sea:

Navigating
Listing Content
Basic File Manipulation
Read the --help output of the following commands:

ls
cd and pwd
echo
seq
cat, head, and tail
pushd and popd
cp and mv and rm
mkdir and rmdir
date
Exercise: Explain pushd and popd; what data structure represents your directory history? Give an example of using them to organise a folder with music.

Exercise: Draw a partial tree of your filesystem, starting from the children of your home directory. Include ancestors of your home directory, and siblings of those ancestors. Exclude files, just show directories. Here is mine:

  (root)/
    |
    | - bin/
    | - boot/
    | - etc/
    | - dev/
    | - home/
    |     | - nlhowell/
    |     |      | - mail/
    |     |      | - media/
    |     |      | - passport/
    |     |      | - src/
    |     |      | - travel/
    |     |      | - usr/
    |     |      | - work/
    |     |
    |     | - spamd/
    |
    | - lib/
    | - lost+found/
    | - mnt/
    | - opt/
    | - proc/
    | - root/
    | - run/
    | - sbin/
    | - sys/
    | - tmp/
    | - usr/
    | - var/
    

Exercise: read the vim normal mode grammar.

vim also has a reasonably sophisticated plugin system; for example, my web browser and mail client are plugins for vim. vim can be used for spreadsheets, pdf creation, website authoring, programming in most languages, etc. Plugins can also extend vocabularies with new verbs, nouns, and prepositions.

Shell scripting

Read Introduction, Basics, and Beyond the Basics from the Advanced Bash-Scripting Guide.

Exercise: Write a shell script that asks the user for their name, and greets them. Sample interaction:

$ bash ./greeter
What's your name? <RETURN>
What's your name? Hippopotamus
Hello, Hippopotamus!
$ 
Exercise: Write a shell script that performs "ROT13" (Caesar cipher with shift 13.) For English, encryption and decryption are the same! (Explain why!) Sample interaction:

$ echo hello | bash ./rot13
uryyb
$ echo uryyb | bash ./rot13
hello
$ echo hello | bash ./rot13 | bash ./rot13
hello
Exercise: Write a shell function that prints "hidden" if the current directory starts with a dot ".", or if any parent starts with a dot. (Files and directories that start with dots are considered "hidden" on many UNIX-like systems.) Sample interaction:

$ pwd
/home/nlhowell
$ bash ~/hidden
$ mkdir .secretdir
$ cd ./.secretdir
$ bash ~/hidden
hidden
$ 


