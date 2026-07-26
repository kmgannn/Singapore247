# Arrays, Memory, and Sorting Algorithms

### 1. Passing Arrays (`int *tab` and `int size`)
* **`int *tab` (The Start of the Hallway):** Just like a string is a hallway of characters where `char *` points to the first room, `int *tab` is a piece of paper pointing to the first box in a hallway of integers (`tab[0]`, `tab[1]`, etc.).
* **`int size` (The Length of the Hallway):** Unlike strings, integer hallways **do not** have a `\0` exit sign at the end. If you only had `int *tab`, you wouldn't know if the hallway had 5 rooms or 5,000 rooms. That is why functions require `int size`—to tell you exactly how many boxes are in the hallway.

---

### 2. Swapping Sticky Notes vs. Swapping Memory
If you have two sticky notes in your hand (`i = 0` and `index = 4`) and you swap the numbers on your sticky notes so `i` becomes 4 and `index` becomes 0:
* **Did the people in the rooms move?** No! John and Alice are still sitting in their original rooms (`tab[0]` and `tab[4]`). You only swapped the numbers on your sticky notes.
* To physically move data, you **must** use brackets to reach into the hallway:
```c
int temp = tab[i];     // Put John in the waiting room
tab[i] = tab[index];   // Move Alice into John's room
tab[index] = temp;     // Move John into Alice's room
```

---

### 3. Min-Max Selection Sort (The "Traffic Cones" & "Scout")
* **The Traffic Cones (`front` and `back`):** Two frozen statues placed at the boundaries of the unsorted mess (`front = 0`, `back = size - 1`). They never move during scouting!
* **The Single Scout (`i`):** One scout walks from the left cone to the right cone. At every box, he checks two things: *"Are you smaller than my record smallest?"* and *"Are you bigger than my record biggest?"*
* **The Illusion of "Doing Twice as Much Work":** Sorting from both ends cuts the number of rounds in half, but requires asking twice as many questions per round. The total amount of computer work ($O(n^2)$) is identical! 1-direction sorting is preferred in practice because it avoids "collision traps" (where swapping the minimum accidentally moves the maximum) and requires half the variables.

---

### 4. Bubble Sort (Comparing Neighbors)
Bubble Sort mimics lining people up by height by comparing next-door neighbors.
* **The Neighbor Comparison:** Compare `tab[i]` directly against the room next door (`tab[i + 1]`). If the left neighbor is bigger, swap them!
* **Stopping Before the Cliff:** The scout must stop at `i < size - 1`. If `i` reaches the very last room, checking `tab[i + 1]` tries to open a room that doesn't exist and causes a segmentation fault / stack smashing!
* **Repeating the Walk:** A single walk down the hallway only guarantees that **one** number (the biggest) bubbles to the very end of the line. To sort all numbers, we wrap the walk in an outer loop (`while (turn < size)`) and place `int i = 0;` inside so the scout gets fresh legs and resets to the starting line on every single turn:

```c
void ft_sort_int(int *tab, int size)
{
    int turn = 0;
    while (turn < size)
    {
        int i = 0; // Scout resets to room 0 for every turn!
        while (i < size - 1)
        {
            if (tab[i + 1] < tab[i])
            {
                int temp = tab[i];
                tab[i] = tab[i + 1];
                tab[i + 1] = temp;
            }
            i++;
        }
        turn++;
    }
}
```
