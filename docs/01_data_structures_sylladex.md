# Data Structures: The Sylladex

The sylladex is Homestuck's inventory system. Every character has one. But the interesting part is that how you store and retrieve items depends on which fetch modus you have active, and every single fetch modus is a real computer science data structure with a real name.

This is not a coincidence. Andrew Hussie was a programmer before he made this comic. He just never put a label on it for the reader.

---

## Stack

**What it is in plain terms:** A stack is a pile. You can only grab from the top. The last thing you put in is the first thing you can take out. This is called LIFO: Last In, First Out.

**Who uses it:** John Egbert, as his default modus at the start of the comic.

**What happens in the comic:** John captchalogues a bunch of items and immediately cannot get to the ones he put in first. He has to eject everything off the top to reach what he actually wants. This is not poor game design. That is exactly how a stack behaves.

**Concrete example:** Imagine you are loading plates into a narrow cabinet one by one. You can only ever grab the plate you put in most recently. The plate at the bottom is stuck until you remove every single plate above it. John's hammer is that bottom plate.

**The CS term:** Stack. LIFO (Last In, First Out). Common in how programs manage function calls. When you call a function inside a function inside another function, the computer stacks those calls and unwinds them in reverse order.

---

## Queue

**What it is in plain terms:** A queue is a line. First person in line is first person served. This is called FIFO: First In, First Out.

**Who uses it:** Also John, via the Queue card found in a book literally called "Data Structures for Assholes."

**What happens in the comic:** Items enter at the top but can only exit from the bottom. Since John keeps stacking new items on top, the oldest item is always the most accessible. The opposite problem from the stack. Now he cannot reach the thing he just picked up.

**Concrete example:** You are printing documents at a printer. The first document you sent prints first. The thing you just sent is waiting at the back of the line. John's sylladex is that printer, except items occasionally get launched at high velocity when the deck is full.

**The CS term:** Queue. FIFO (First In, First Out). Used in things like task scheduling, where you want to process requests in the order they were received.

---

## QueueStack (Deque)

**What it is in plain terms:** A double-ended structure where you can pull from either side.

**Who uses it:** John, after combining both cards with his Modus Control Deck.

**What happens in the comic:** John creates a grid of smaller queuestacks. He can draw from the top or bottom of any of them. He basically built himself a more flexible inventory by merging two contradictory systems.

**The CS term:** Deque (double-ended queue, pronounced "deck"). This is a real data structure. You can add or remove from either end.

---

## Binary Tree

**What it is in plain terms:** A tree structure where each node has at most two children: one to the left, one to the right. Items are sorted by a rule that puts smaller values left and larger values right.

**Who uses it:** Rose Lalonde, who describes her modus as "elegant."

**What happens in the comic:** The first item she captchalogues becomes the root. Every new item becomes a branch attached to an existing card, going left or right based on alphabetical order. Items at the end of all branches are called leaves. Removing the root drops everything. Removing a branch drops everything below it.

**Concrete example:** Imagine a filing system shaped like an upside-down tree. You file "Banana" first. That is the trunk. "Apple" comes in: it goes left because A comes before B. "Cherry" comes in: it goes right because C comes after B. Now "Apricot" arrives: it checks the trunk (before B, go left), checks Apple (after A, go right), and hangs there. Every lookup follows the same path. It is fast for sorted retrieval and painful if you remove something in the middle.

**The CS term:** Binary Search Tree (BST). The rule Rose uses is alphabetical ordering, which is a valid BST comparator.

---

## Hash Map

**What it is in plain terms:** A structure that stores items by converting a key into a number (called a hash), then using that number as a slot index. The point is fast lookup. You do not search through everything. You just compute where it should be and go there directly.

**Who uses it:** Dave Strider.

**What happens in the comic:** Dave's modus assigns each letter a value (vowels = 1, consonants = 2 by default). When he wants to store an item, he calculates the total value of its name, divides by the number of cards in his deck, and the remainder is the slot index. To retrieve it, he has to say something with the same hash value. He once ejected his ninja sword by yelling "stop" at a bird because "stop" and "ninja sword" hashed to the same slot index.

**The collision problem:** If two different items hash to the same slot, one gets ejected to make room. This is a hash collision. Dave's modus has a "detect collisions" checkbox that, when enabled, prevents new items from overwriting existing ones. That is a real collision handling strategy called collision detection.

**Concrete example:** You have ten lockers numbered 0 to 9. Your locker rule is: count the letters in an item's name, mod 10, that is your locker. "Pen" has 3 letters, so it goes in locker 3. "Cup" also has 3 letters. Collision. One of them gets pushed out. Dave lives this daily.

**The CS term:** Hash Map (also called Hash Table). The process of converting a key into an index is hashing. The leftover from division is the modulo operation.

---

## Array

**What it is in plain terms:** An indexed list where every slot is directly accessible at any time. No rules about order. No forced retrieval path.

**Who uses it:** John, after upgrading from Stack and Queue.

**What happens in the comic:** He can captchalogue any item into any card and retrieve any card at any time. It is the most boring and most practical fetch modus. John had it available as a birthday present the whole time.

**The CS term:** Array. The most basic data structure. Fixed-size, indexed, constant-time access. Everything else in this file is a more constrained version of this.
