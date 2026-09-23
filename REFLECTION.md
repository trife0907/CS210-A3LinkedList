### 1. In LinkedList::deleteFront(), why does it take two separate delete calls instead of one? Name exactly what each one frees, and name the two new calls back in the program responsible for putting them on the heap in the first place.
This function takes two delete calls because the node holds another pointer inside of it. `delete doomed->data;`
frees the data value, and `delete doomed;` frees the node. The two `new` calls responsible for these deletes are 
`list->addFront(new int());` in `main.cpp` and `Node<T>* fresh = new Node<T>(value);` in `LinkedList.h`.

### 2. ArrayList never had a destructor before today. Explain, in your own words, why switching from T data[CAPACITY] to T* data [CAPACITY] is what made a destructor necessary, and what would happen if you forgot to write one. Would you get a compiler error? Why or why not?
Switching to an array of pointers made a destructor necessary because every element we add to the stack gets created 
the `new` keyword, which means it's allocated on the heap and must be deleted manually. If we forgot to write a 
destructor, the code would still compile because destruction doesn't affect anything syntax-wise, but we would cause a 
memory leak, eventually causing the program to crash.

### 3. search() and addFront() both take a T*, but they treat that pointer completely differently. Explain the difference in terms of ownership: which one is allowed to delete what you hand it, and which one is never allowed to?
`addFront()` is allowed to delete what you hand it because it takes ownership. `search()` is never allowed to delete 
because it is a `const` function and it only looks through each object, but never tampers with them.

### 4. You swapped LinkedList<T> for ArrayList<T> inside makeList() and reran main.cpp without changing a single line there. What two mechanisms, by name, made that possible?
The two mechanisms that make this work are the `makeList()` function, which allows for a different type of list to be 
created at runtime, and the use of the `virtual` keyword for all the functions in `List.h`. Because both LinkedList and 
ArrayList inherit from List, `virtual` lets the List object the correct function to call at runtime.

### 5. Pick one keyword from the Key Terms glossary that you either had to add today or wouldn’t have thought to add on your own (explicit, override, virtual, const, or any other). Describe, in your own words and without copying the guide’s wording, the smallest example you can think of where leaving it out would cause a real problem.
One keyword I wouldn't have thought to add on my own was the `virtual` keyword. When working with Java, runtime 
polymorphism already determines what the correct function to call when dealing with inherited classes, but here,
we must implement this feature manually using this keyword. If we were to leave it out, I can imagine a scenario where 
we implement a List-type pointer as a LinkedList, and try to make function calls. The functions would never execute 
because it doesn't know which object's functions to call, since List's functions are purely abstract.