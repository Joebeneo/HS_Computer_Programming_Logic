# Sollux's ~ATH Code Review

_In which the characters of Homestuck try to understand a programming language where the only control flow is death._

---

## Program 1: The Universe Bomb

This is the actual program used in the comic to summon Lord English. Let us walk through it line by line.

```
import universe U;

~ATH(U) {

} EXECUTE(NULL);

THIS.DIE();
```

**Line by line:**

| Line | What it does |
|------|-------------|
| `import universe U;` | Brings the concept of "the universe" into scope and names it `U` |
| `~ATH(U) {` | Opens a loop bound to `U`'s lifespan. Runs as long as `U` is alive |
| `} EXECUTE(NULL);` | When `U` dies (universe ends), execute `NULL` (do nothing) |
| `THIS.DIE();` | Kill the program itself |

**What this program does in human terms:** Wait for the universe to end. When it ends, do nothing, then terminate.

**What this program actually does in Homestuck:** It runs for the entire lifespan of the universe. When the universe is destroyed, the EXECUTE fires. The "nothing" it executes is not nothing. It is the trigger for Lord English's entry into the universe at the moment of its death. The act of the program ending IS the event.

Think of it as a deadman's switch. The program's only purpose is to stop running. And when it stops, that means something happened.

---

## Program 2: Karkat's Infinite Rage

```
import universe U;
import author Karkat;

~ATH(U) {
  ~ATH(Karkat) {
  } EXECUTE(NULL);
} EXECUTE(NULL);

THIS.DIE();
```

The file name is `AAAAAAAAAAAAAUUUUUUUUUUUUUUUGH.~ATH`. The file extension for ~ATH programs is `.~ATH`. Karkat named his program a scream.

**Nested loop breakdown:**

```
OUTER LOOP: runs while Universe is alive
│
├── INNER LOOP: runs while Karkat is alive
│   │
│   └── When Karkat dies → EXECUTE(NULL)
│
└── When Universe dies → EXECUTE(NULL)

After both loops end → THIS.DIE()
```

**The dependency:** The inner loop (Karkat) can only run while the outer loop (Universe) is also running. If the universe dies first, both loops end. If Karkat dies first, only the inner loop ends, and the outer loop continues until the universe also ends.

**In real programming terms:** This is a nested while loop.

```python
# Pseudocode translation
while universe.is_alive():
    while karkat.is_alive():
        pass  # do nothing
    on_karkat_death()  # EXECUTE(NULL)
on_universe_death()    # EXECUTE(NULL)
terminate()            # THIS.DIE()
```

The ~ATH version is more dramatic about it.

---

## Program 3: Sollux's Bifurcation Bomb

```
bifurcate THIS[THIS, THIS];
import universe U1;
import universe U2;

~ATH(U1) {
  ~ATH(!U2) {
  } EXECUTE(~ATH(THIS){}EXECUTE(NULL));
} EXECUTE(~ATH(THIS){}EXECUTE(NULL));
```

This one is dense. Let us break it apart.

**`bifurcate THIS[THIS, THIS];`**

Split the current program into two branches. Both are called `THIS` (they are copies of the same program). This is ~ATH's version of forking a process or spawning a thread.

**`import universe U1; import universe U2;`**

Import two separate universes. In Homestuck's cosmology, multiple universes exist simultaneously. This program binds to two of them.

**`~ATH(U1) { ... }`**

Outer loop: runs while Universe 1 is alive.

**`~ATH(!U2) { ... }`**

Inner loop: runs while `NOT U2` is alive. The `!` inverts the condition. `!U2` means "the state where U2 does not exist." This loop runs as long as U2 does NOT exist, and terminates when U2 begins to exist.

**`EXECUTE(~ATH(THIS){}EXECUTE(NULL));`**

When the loop ends, execute... another ~ATH loop. This creates a new loop bound to `THIS` (the program itself) that immediately executes NULL and presumably terminates. It is a self-referential teardown. The program's death triggers a sub-program whose death triggers nothing.

**The whole thing in sequence:**

```
1. Fork into two threads
2. Thread runs: wait for U1 to exist AND U2 to not exist
3. When U2 comes into existence → inner loop ends
4. Fire a self-destructing sub-loop
5. When U1 dies → outer loop ends
6. Fire another self-destructing sub-loop
7. Both threads do this simultaneously
```

---

## What Sollux Would Say About It

> **TA: ok 2o here2 the thiing about ~ath.**
> **TA: every program you wriite iin iit ii2 ba2iically a bomb wiith a tiimer.**
> **TA: the tiimer ii2 not a number. the tiimer ii2 the liifespan of a concept.**
> **TA: you dont get two 2ay "run for 10 2econd2." you get two 2ay "run untiil thii2 per2on diie2."**
> **TA: or "run untiil thii2 uniiverse end2."**
> **TA: iit2 the only language where the haltiing problem ii2 liiterally about death.**
> **TA: the haltiing problem iin CS a2k2: can you predict whether a program wiill ever 2top runniing?**
> **TA: iin ~ath the an2wer ii2: iit 2top2 when 2omethiing diie2. can you prediict death?**
> **TA: no. no you cannot.**
> **TA: 2o every ~ath program ha2 an undetermiinii2tiic runtiime and that2 not a bug iit2 the whole poiint.**

---

## What Karkat Would Say About It

> **CG: I WROTE A PROGRAM IN THIS LANGUAGE ONCE.**
> **CG: I NAMED IT AFTER THE SOUND I MAKE EVERY TIME I THINK ABOUT THE FACT THAT I WROTE A PROGRAM IN THIS LANGUAGE.**
> **CG: THE PROGRAM DOES NOTHING. IT LOOPS FOREVER UNTIL I DIE AND THEN IT DOES NOTHING AGAIN.**
> **CG: THAT IS NOT A JOKE. THAT IS WHAT THE CODE SAYS. I CHECKED.**
> **CG: SOLLUX TOLD ME IT WAS "ELEGANT" AND I TOLD HIM TO GO BIFURCATE HIMSELF.**
> **CG: WHICH IN RETROSPECT IS AN ACTUAL ~ATH COMMAND SO HE PROBABLY TOOK IT AS A COMPLIMENT.**
> **CG: THE ENTIRE LANGUAGE IS A MONUMENT TO THE IDEA THAT PROGRAMMERS SHOULD NOT BE ALLOWED TO NAME THINGS.**
> **CG: "TIL DEATH." WHO APPROVED THIS. WHO LOOKED AT A PROGRAMMING LANGUAGE AND SAID YES THE FUNDAMENTAL UNIT OF COMPUTATION SHOULD BE MORTALITY.**
> **CG: I AM GOING TO WRITE A LOOP THAT RUNS UNTIL MY PATIENCE DIES, WHICH MEANS IT ALREADY TERMINATED FOUR SENTENCES AGO.**

---

## The Destructor Connection, Explained

In C++, when an object is destroyed, a special function called the destructor runs automatically. It is marked with a tilde:

```cpp
class Universe {
public:
    Universe() {
        // constructor: runs when Universe is created
    }
    ~Universe() {
        // destructor: runs when Universe is destroyed
        summonLordEnglish();
    }
};
```

The `~` in `~Universe()` means "this function fires when Universe dies."

The `~` in `~ATH` means "this entire language is about things dying."

~ATH is a language where every program is a destructor. There are no constructors. There is no building. There is only the act of binding your logic to something's eventual nonexistence and waiting.

---

## Translation Table

| ~ATH Concept | Real Programming Equivalent |
|---|---|
| `~ATH(X) { }` | `while(X.isAlive()) { }` |
| `EXECUTE(action)` | Callback function that runs after the loop ends |
| `import concept X` | Dependency injection / importing a module |
| `THIS.DIE()` | `process.exit()` / `System.exit()` |
| `bifurcate` | `fork()` / spawning a thread |
| `!X` | Logical NOT / inverse condition |
| `.~ATH` file extension | Just vibes, honestly |

---

## Try It Yourself

Write the pseudocode translation of this ~ATH program:

```
import planet Earth;
import star Sun;

~ATH(Sun) {
  ~ATH(Earth) {
  } EXECUTE(NULL);
} EXECUTE(NULL);

THIS.DIE();
```

<details>
<summary>Answer</summary>

```python
while sun.is_alive():
    while earth.is_alive():
        pass
    # Earth has been destroyed (but Sun still exists)
    do_nothing()
# Sun has died
do_nothing()
terminate()
```

The program waits for Earth to be destroyed (inner loop ends), then waits for the Sun to die (outer loop ends), then terminates.

If the Sun dies before Earth, both loops end simultaneously (outer loop death kills the inner loop too). If Earth is destroyed first, the outer loop keeps running in an empty state until the Sun also goes.

This is cosmologically accurate. The Sun will eventually die. If something destroys Earth first, the Sun will keep going until it doesn't. ~ATH does not care about your feelings about this.

</details>
