# Chapter X: Stacks & Queues
Stacks and queues are very simple data structures.

You can imagine a stack as a stack of plates. When you create a stack, you start by adding the
first plate at the bottom and then build up the stack. When you remove a plate, you remove a plate 
from the top of the stack and not the bottom since it's easier to do.

In other words, with a stack, the order of insertion/deletion can be encapsulated by the following
phrase: *first in, last out*. The time complexity of a stack reflects this; adding to the stack is
`O(1)` and deleting from the stack is `O(1)`, of course with the *first in, last out* limitation.
