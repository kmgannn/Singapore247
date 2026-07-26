# Strings and Pointers: The Hallway Analogy

In C, **C does not actually have "strings".** 
A string is just a bunch of characters placed side-by-side in memory, ending with a special invisible character called the **null terminator** (`\0`).

Imagine a string is a hallway of connected hotel rooms.

If you have the string `"Hello"`:
* Room 101 contains `'H'`
* Room 102 contains `'e'`
* Room 103 contains `'l'`
* Room 104 contains `'l'`
* Room 105 contains `'o'`
* Room 106 contains `'\0'` *(This tells the computer "STOP, the text ends here")*

### How the Character Pointer (`char *`) Works
When a function asks for a `char *` (a character pointer), it is simply asking for a piece of paper that tells it **where the hallway starts**. 

When you do this:
```c
print_string("Hello");
```
The computer creates the hallway of rooms for "Hello" in memory, and then it hands your function a `char *` pointer containing the address of the very first room (Room 101).

### How it translates to printing
Once the function has that starting address, it uses pointer math to walk down the hallway. Because characters are exactly 1 byte in size, moving to the "next address" is as easy as adding 1 to the pointer.

Here is exactly how a basic print function does it under the hood:
```c
void print_string(char *str) 
{
    int i = 0;
    
    // Keep looping until the room we look inside contains the '\0' stop sign
    while (str[i] != '\0') 
    {
        // Go inside the room at address (str + i), grab the character, and print it
        write(1, &str[i], 1); 
        
        // Move to the next room down the hallway
        i++;
    }
}
```
Passing a `char *` doesn't pass the whole string—it just passes the **starting address**. The function then takes that address, prints the character there, steps forward to the next address, prints it, and keeps walking forward until it hits the `\0`!
