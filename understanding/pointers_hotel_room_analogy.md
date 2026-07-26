# Pointers: The Hotel Room Analogy

Think of variables as **physical boxes on a shelf** (or hotel rooms).

### 1. The Setup (The Box/Room)
```c
int b = 5; 
```
* You rented a hotel room named **`b`**. 
* Inside room `b`, you put the number **`5`**.
* Let's say the operating system placed this box on the shelf at **address `0xE`**.

### 2. Creating the Pointer (A Piece of Paper)
You want to give your friend instructions on how to find room `b`. You need a piece of paper to write the room number on. 
```c
int *ptr;
```
* `int *ptr` simply means: *"I am creating a blank piece of paper named `ptr` that is meant to hold a room number."*

### 3. Getting the Room Number
Right now, the paper is blank. We need to write `b`'s room number on it. We use `&` to mean *"get the room number of"*.
```c
ptr = &b;
```
* Now, your piece of paper (`ptr`) has `b`'s room number written on it.

### 4. Changing the Value (Opening the Door)
You want to kick the `5` out of the room and put a `56` in there, but you only have the piece of paper (`ptr`). 
To do this, you use the `*` symbol. When used *here*, the `*` acts as a master key. It means *"Go to the room written on this paper, and open the door."*
```c
*ptr = 56;
```
* The computer looks at the paper (`ptr`).
* It walks to that room (`b`).
* It opens the door, takes out the `5`, and puts in `56`.

---
### Changing the Address vs. Changing the Value
If `a` and `b` are pieces of paper with room numbers on them:
Doing `b = &div2` just erases the room number on the paper and writes a new room number on it. It **does not** change the value inside the actual room.
If you want to reach into the original room and change the value, you **must** use the `*` master key to open the door:
```c
*a = temp_div;
*b = temp_mod;
```

---
### Why use `**super_ptr`? Why not point directly to the integer?
If your goal is just to reach the integer `5`, you **should not** use a double pointer (`**`). You would just create a second normal pointer and give it the address of the integer.

You ONLY use a double pointer when you need to change the *middleman*. 
Imagine `ptr1` is currently pointing to `num`. What if you want to write a function that changes `ptr1` so that it points to a *different* variable instead? 
To change what `ptr1` contains, you need the address of `ptr1` itself. That is the only scenario where you use `int **`.
