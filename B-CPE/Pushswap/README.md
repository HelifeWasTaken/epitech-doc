# PushSwap

## Prerequirities

Make sure you understand well the linked list principle and the Push and Pop methods

If you have them in mind the Push Swap is a piece of cake and you can implement a bubble sort with 3 files (less than 15 functions)

You can try implementing Stacks Queues and Deques so the project will fell easier

If you can do so It will be really easy to implement the rest of the project

## The algorithm

Forget about QuickSort it is impossible to do it with the possibles interactions given

Something that could be somewhat implemented is the merge or insertion sort with a bit of divide and conquer

PushSwap has been made so you could not just copy some random sorting algorithm and implement it so be creative!

Of course always try first with bubble sort (it works better than you think)

## Over-engineering

You could do bufferisation!

As you might certainly have done you have written everytime that is pretty pretty rough for your computer

So you could use bufferisation to make your program faster

The principle is just to store up to generally 4096 in a `char *` or `char[4096]` (it 's even better) and everytime it is full of at least 4095 you print it and empty the buffer
It coudl consequently upgrade the time of your algorithm
