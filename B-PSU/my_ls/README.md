# my_ls

## Prerequirities

The project assumes that you already understand how to deal with arrays how example filter them and how to use basic structs

## The start:

The first you should do is to print the list of files in the folder

This project is one of the first that makes you deal with syscall such as:
```c
DIR *opendir(const char *name);
int readdir(unsigned int fd, struct old_linux_dirent *dirp,
        unsigned int count);
(stat etc...)
```
Make sure to check the return value of your functions as some unix permissisons might be tricky!
It is not because stat suceeded for example that you can open the folder without checking the return value!

Some important resources:
    - man 2 stat
    - man 3 stat
    - man opendir
    - man readdir
    - man access
    - man inode

## The parsing

Once you built your basic ls that just list the current directory or the one specified you can start the parsing

The one thing important to know in unix is how arguments are given

The most simple and easy and efficient parsing possible is juste to check for the first character if it is a '-' you can try to check if it is an option

For example you could as for the start try to separate the arguments options from the regular ones so:

`ls -l toto -d tata -la -h`

Should return something like:
```c
// The first argument is the binary name so it is skipped

// Array of regular arguments
[toto, tata]

// Array of options
[-l, -d, -la, -h]
```
Then the you should just iterate your arrays of options and for each character in it except the "-" try to activate a flag

If one flag is invalid just tell the user right away and exit the program by returning if exit is not allowed

Of course you should stock all your flags info in a struct like so:

```c
// For example
struct flag_info {
    int l_flag;
    int d_flag;
    int a_flag;
    int h_flag;
    ...
};
// Thoses can be done by a simple switch case or functions pointers
```
It is the most easy way to store data as you don't have a lot flags to deal with

Some might use bitwise operation but it is kind of too overkill to use that

Remember that: `ls -l` and `ls -l -ll -l` does the same thing and activate just once the -l flag

## To go further

You might be starting to be a little confused because you must do stuff like handling multiples args or even doing the recursive -R !

If you have this kind of problems try to look first about linked list to store your data try to preparse your data before printing it and store it somewhere

Then make sure all of your functions are single resonsibilities it will help for the recursive calls

Then try to activate some special pattern printing with some types of boolean

For example your printing functions might do some lot of boolean checks on your flags before printing and change the parsed data

Your ls function should received the whole information about flags and if recursive status is currently happening

Something such as boolean like:

```c
int my_ls(struct data_pre_parsed *data, bool is_in_recursion_state);
```

Or you could call it `my_ls_internal` if you absolutely want to parse data in the my_ls function and have your main just calling my_ls

## The key of the success:

Understand pointers and arrays
Maybe linked list but it can still be done with arrays

Read the doc like really timestamp and inodes requires a lot of attention

Write unit tests
