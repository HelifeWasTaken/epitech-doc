# SHELL PROGRAMMING

## Minishell1

The minishell project will introduce you to the world of low level programming

Here you will learn about essentials stuff such as forks, pid, jobs, program executions

### Prerequisites

    - Make sure to read carefully the documentation!
    - Know the basics of parsing and make sure to know how to split a string
    - Check your memory allocations
    - Do not leak the files descriptors
    - Check your system calls (thoses are the 2nd reason of why your minishell timeout/crashes the first one being bad parsing)

### Resources
    - man 2 waitpid
    - man 2 _exit
    - man 2 fork
    - man 2 signal
    - man 2 wait4
    - man 2 execve
    - man 3 exec
    - man errno

Make sure to read importants stuff about ERRORS sections and RETURN sections thoses will save your life

Keep in mind that minishell2 and 42sh are the next project and your minishell might be prone to change completely if the codebase is not flexible enough so please do not hard code the stuff in

MAKE SURE TO KNOW HOW TO USE STRUCTS

Here is a simple start that won't make you go further than the 60-70%: [here](https://brennan.io/2015/01/16/write-a-shell-in-c/)

If you are REALLY comfortable with this and want to start looking forward to msh2 and 42sh here is a solid start - Harm Smith: [Here](https://www.cs.purdue.edu/homes/grr/SystemsProgrammingBook/Book/Chapter5-WritingYourOwnShell.pdf)

## Minishell2

### Prerequisites

You know how to use linked list and recursion and you know it well
Further more your minishell-1 passes at least 80%

### The AST:

Here you are you have a super minishell1 but except if you are the type of guy writing a single function does a single responsibility you might redo your shell from scratch

But hey now that you are here you might have heard about redirections

If you are here I should be better that you know what is an AST or abstract syntax tree if you don't then it's the time to learn

You could still do the project without it but I don't want to bother explaining the hassle to do that and then porting it to the 42sh

Here is the shell grammar in Backus-Naur form:
```
<command line>	::	<job>
		|	<job> '&'
		| 	<job> '&' <command line>
		|	<job> ';'
		|	<job> ';' <command line>

<job>		::=	<command>
		|	< job > '|' < command >

<command	::=	<simple command>
	        |	<simple command> '<' <filename>
	        |	<simple command> '>' <filename>

<simple command>::=	<pathname>
	        |	<simple command>  <token>
```

The ast is recurive binary tree with generally looks like that:
```
struct ast {
    int type;
    struct data_info data;
    struct ast *left;
    struct ast *right;
};
```

Of course data_info is not a real valid name chose a better one for your struct

(AST of a regular shell expression)[https://files.gogaz.org/2min_42sh_html_7e077d9d7067f208.png]

The AST should be recursively called from left to right following the operators logic

This type of Data structure will help you know easily when there is a problem in the syntax of your program for example: `&& or || or >` are badly used

### Redirections:

Redirections can be tricky and have some odd priorities make sure to know well how thoses are made
If your ast is well built then there should be no problem when evaluating everything (it should be auto with an int)

Remember that until the end of the redirection by pipes everything must be async and done recursively to handle the multi pipe

Some resources:
    - man 2 open
    - man 2 dup
    - man 2 dup2
    - man 2 write
    - man 7 fifo
    - man 7 inode
    - man 2 stat
    - man 2 close

And of course [the reference](https://www.cs.purdue.edu/homes/grr/SystemsProgrammingBook/Book/Chapter5-WritingYourOwnShell.pdf)

MAKE SURE TO NOT LEAK ANY FILE DESCRIPTORS TO CLOSE EVERYTHING AND TO CHECK EVERY SYSCALL !!!!

### 42sh

Nothing to say except you should learn how to use ncurses if you don't know how to use it
And of course [the reference](https://www.cs.purdue.edu/homes/grr/SystemsProgrammingBook/Book/Chapter5-WritingYourOwnShell.pdf)
To implement all the things that you did not such as jobs that are not that hard to implement
