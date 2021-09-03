# my_printf

## Basics:

The printf project is one of the basic knowledge about `va_args` and `va_list`

The first thing to be understood is to know how to use thoses variadic arguments

See: `man 3 va_arg`

For example try to do a function that prints n number with the following prototype

```c
void print_n_numbers(int n, ...);
```

Of course you should pass also n integers so your program won't crash when you try to access thoses numbers

The next thing that you should know is parsing

The printf format is always the same for the basics one: `%d` `%c` `%%`

Each of theses do a special thing

For the starters you could do something like:

```py

def run_my_printf_cmd():
    if this is a 'd':
        run_int_print_function()
    elif this is a 'c':
        run_char_print_function()
    elif ...:
        ...
    else:
        print(current_char)

def my_printf():
    while not at the end:
        if current_char is a '%':
            go_to_next_character
            run_my_printf_cmd()
        else:
            print_current_char()
```

If I find a '%' I start by looking if there is an another character after

If there is not print a '%'

Then if this one of the flags known (see `man 3 printf` flag section) then do the action

If this is not print the the two characters and proceed

To do so you should have one function that checks if the current character is a '%' run the flag function that will check the current flag else print the current char

## Advanced Stuff:

Make sure you understand well and have a clear of how to do the stuff above

As this is the first project you might not be really familiar with structs but thoses are important stuff notably to store a lot of data

Make sure to know how to use them then come back later!

So now you understand the basics of structs and maybe pointers to struct which would be super great!

So know you are ready to try to parse stuff such as %ld

Printf can have some special flags that are called length modifiers so the information while parsing must be stored somewhere

Enum can be a great choice to know how to parse thoses types of things and can be stored on a struct

So the parsing now should be :

```
Check if there is a percentage

Check if there is a length modifier and store the value if there is one

Check if the current character is a valid printf flag

Do an exception case if the current char is not a valid printf flag else launch the command
```

But the one problem you might say now is that when your command is finished you cannot foward by two chars
Because some length are really big such as: %llc that needs to forward by 4

So here are some possibilities:
    1- Return the number of character read on the format (Not recommended because printf needs to return the number printed to have 100% but it can be a valid option if you struggle a lot)
    2- Store the index in struct (Requires to understand pointer to struct and passing a struct as an address)
    3- Using pointers arithmetic on the string (Best one but the most dangerous one and advanced one)

!! Remember that lengths modifiers change the type of the variable used for example %lld transform an int to a long long int

If you can do all of that understood

The last thing that you could implement to do really beautiful code is functions pointers

You can look up about that It is one of the most powerful thing that you could use on your whole year

## The chads:

There are also other things such as: `%2s` or `%*.*lf` etc... for the strongest ones !!
I will let you search for thoses one how to implement them

And don't forget to write unit test!
