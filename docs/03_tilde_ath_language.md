# ~ATH: An Esoteric Programming Language

~ATH (pronounced "til death") is a programming language that appears in Homestuck as a language characters actually write code in. It is fictional but internally consistent enough that the programming community has analyzed and partially reverse-engineered its rules.

It is also genuinely one of the weirder language concepts you will find anywhere, fiction or otherwise.

---

## The Core Rule

Every program in ~ATH is built around one construct: a loop that runs until something dies.

```
~ATH(X) {
// stuff to do while X is alive
} EXECUTE(something);
```

You import a concept, bind the loop to its lifespan, and whatever is inside the loop runs until that concept ceases to exist. Then `EXECUTE` fires once, at the end.

There is no `while (condition)`. There is no `for i in range`. There is only: wait for death, then act.

---

## Imports

Before you can bind a loop to something, you have to bring it into scope:

```
import universe U;
~ATH(U) {
} EXECUTE(NULL);
THIS.DIE();
```

This program does nothing until the universe ends, then executes NULL and terminates. This is the program used to summon Lord English.

Importing in ~ATH works like importing in real languages: you are giving a name to an external concept so you can reference it in your code. The difference is that instead of importing a library or a module, you are importing the abstract concept of a living thing and binding your logic to when it stops existing.

---

## Nested Loops

Loops can go inside other loops. The inner loop only runs while the outer loop is also running.

```
import universe U;
import author Karkat;

~ATH(U) {
  ~ATH(Karkat) {
  } EXECUTE(NULL);
} EXECUTE(NULL);

THIS.DIE();
```

This is Karkat's `AAAAAAAAAAAAAUUUUUUUUUUUUUUUGH.~ATH`. The inner loop runs as long as Karkat is alive, but only during the outer loop's execution, which runs as long as the universe is alive. Two nested death conditions.

In real programming this maps to nested loops: a loop inside a loop, where the inner one completes its full cycle for every single iteration of the outer one.

---

## Bifurcation

Sollux's code introduces `bifurcate`, which splits the program into two labeled branches that run as separate concurrent loops.

```
bifurcate THIS[THIS, THIS];
import universe U1;
import universe U2;

~ATH(U1) {
  ~ATH(!U2) {
  } EXECUTE(~ATH(THIS){}EXECUTE(NULL));
} EXECUTE(~ATH(THIS){}EXECUTE(NULL));
```

`!U2` means the inverse of universe U2: the loop runs until the non-existence of U2 ends, which is when U2 begins to exist. This is using logical NOT on an imported concept.

Bifurcation in ~ATH is the closest thing it has to threads or subroutines. You split execution into two named branches that can be referred to and manipulated individually.

---

## The Tilde and Destructors

The tilde prefix in ~ATH is not accidental. In C++, the tilde is used to mark a destructor: a function that runs when an object is destroyed and cleaned up from memory. `~MyClass()` fires right before the object stops existing.

~ATH takes this one step further and makes the destructor the entire language. Every program is, in effect, one big destructor waiting to fire.

---

## What Makes It "Esoteric"

An esoteric programming language (esolang) is a language designed to explore the edges of programming language design rather than to be practically useful. ~ATH fits this completely. It has:

- No way to write a short program that does something immediately
- No mutable state
- No conditionals beyond the loop-death check
- Only one command that actually executes anything (`EXECUTE`), and it can only appear at the end of a loop

It is philosophically consistent and computationally absurd.
