# The Alchemy Workshop: Bitwise Fusion in Practice

_In which we take two items, turn them into bits, smash those bits together, and see what comes out the other side._

---

## Before We Start

This workshop uses simplified codes for clarity. Real captchalogue codes are 48 bits long (8 characters at 6 bits each). We will use 8-bit codes here so you can actually follow the math without your eyes glazing over. The logic is identical at any bit length.

---

## Experiment 1: Hammer AND Nail

We are going to AND a hammer with a nail. In the comic, AND is performed by overlapping two punched cards on top of each other. Only holes that exist on BOTH cards survive.

**Hammer code:** `11010110`
**Nail code:** `10011010`

Line them up:

```
Hammer:  1 1 0 1 0 1 1 0
Nail:    1 0 0 1 1 0 1 0
         ─────────────────
AND:     1 0 0 1 0 0 1 0
```

The rule: each bit in the result is 1 only if BOTH inputs are 1.

```
Position 0: 1 AND 1 = 1  ✓ both punched through
Position 1: 1 AND 0 = 0  ✗ nail blocks this hole
Position 2: 0 AND 0 = 0  ✗ neither has a hole here
Position 3: 1 AND 1 = 1  ✓ both punched through
Position 4: 0 AND 1 = 0  ✗ hammer blocks this hole
Position 5: 1 AND 0 = 0  ✗ nail blocks this hole
Position 6: 1 AND 1 = 1  ✓ both punched through
Position 7: 0 AND 0 = 0  ✗ neither has a hole here
```

**Result:** `10010010`

**What happened to the bits:**
- Hammer had 5 active bits
- Nail had 4 active bits
- Result has 3 active bits

AND always produces equal or fewer active bits than the input with fewer bits. You are filtering down to the overlap. The result is a "minimum" of both items.

If Hammer is mostly "structural" bits and Nail is mostly "pointy" bits, the AND result keeps only what they share. You might get a small, precise striking tool. Something like a tack hammer.

---

## Experiment 2: Hammer OR Nail

Same items. Now we punch one card with both items' hole patterns. Any hole from either card ends up in the final card.

```
Hammer:  1 1 0 1 0 1 1 0
Nail:    1 0 0 1 1 0 1 0
         ─────────────────
OR:      1 1 0 1 1 1 1 0
```

The rule: each bit in the result is 1 if EITHER input is 1.

```
Position 0: 1 OR 1 = 1  (both had it)
Position 1: 1 OR 0 = 1  (hammer had it)
Position 2: 0 OR 0 = 0  (neither had it)
Position 3: 1 OR 1 = 1  (both had it)
Position 4: 0 OR 1 = 1  (nail had it)
Position 5: 1 OR 0 = 1  (hammer had it)
Position 6: 1 OR 1 = 1  (both had it)
Position 7: 0 OR 0 = 0  (neither had it)
```

**Result:** `11011110`

**What happened to the bits:**
- Hammer had 5 active bits
- Nail had 4 active bits
- Result has 6 active bits

OR always produces equal or more active bits than the input with more bits. You are combining everything from both inputs. The result is a "maximum" of both items.

This is the kind of combination that produces something like a hammer with a nail built into the striking face. More features. More chaos. More "what even is this."

---

## Experiment 3: The AND Decay Chain

What happens when you AND the same item with itself repeatedly?

```
Item A:         11010110
A AND A:        11010110  (identical, no change)
```

AND with yourself changes nothing. Every bit matches. But what about chaining DIFFERENT items?

```
Item A:          11010110  (5 bits active)
Item B:          10011010  (4 bits active)
A AND B:         10010010  (3 bits active)

Item C:          01010101  (4 bits active)
(A AND B) AND C: 00010000  (1 bit active)

Item D:          11100011  (5 bits active)
((A∧B)∧C) AND D: 00000000  (0 bits active) ← DUD CODE
```

**Four items deep and we hit all zeros.** The code is dead. No item exists there.

This is the AND decay problem. Every AND operation can only turn bits OFF, never ON. Given enough combinations, you inevitably converge toward `00000000`. It is mathematically guaranteed.

---

## Experiment 4: The OR Saturation Chain

The opposite problem:

```
Item A:          11010110  (5 bits active)
Item B:          10011010  (4 bits active)
A OR B:          11011110  (6 bits active)

Item C:          01010101  (4 bits active)
(A OR B) OR C:   11011111  (7 bits active)

Item D:          11100011  (5 bits active)
((A∨B)∨C) OR D:  11111111  (8 bits active) ← ALL ONES
```

**Four items deep and we hit all ones.** In the captchalogue code system, this would be `!!!!!!!!`. Also a dud.

OR saturation. Every OR can only turn bits ON, never OFF. Chain enough together and every bit is lit. The code is maxed out. Nothing useful lives there either.

---

## The Sweet Spot

The best alchemy results come from:
- Combining just two items (minimal chain decay)
- Items with complementary bit patterns (some overlap but not too much)
- Choosing AND vs OR based on whether you want a "refined" or "fused" result

This is why John's early combinations work well (simple two-item fusions) and his late-game attempts produce garbage (long chains of OR combinations that push toward all-1s).

---

## The Visual Version

Here is AND vs OR as a physical card demonstration:

```
CARD A (punched holes shown as ○, solid shown as ●)

● ○ ● ○ ● ○ ● ●
○ ● ○ ● ● ● ○ ○


CARD B

○ ○ ● ● ○ ● ○ ●
● ○ ○ ● ○ ○ ● ○
```

**AND (stack cards, light passes through only shared holes):**

```
● ○ ● ● ● ● ● ●     Only holes that appear in BOTH
○ ○ ○ ● ● ● ● ○     cards let light through.
```

**OR (punch card A with card B's holes added):**

```
○ ○ ● ○ ○ ○ ○ ●     Every hole from either card
○ ○ ○ ● ○ ○ ○ ○     is present in the result.
```

AND = restrictive. OR = additive. That is the whole thing.

---

## Try It Yourself

Given these two 8-bit codes, compute both AND and OR:

**Sword:** `11100101`
**Shield:** `01011110`

<details>
<summary>Answers</summary>

```
Sword:    1 1 1 0 0 1 0 1
Shield:   0 1 0 1 1 1 1 0
          ─────────────────
AND:      0 1 0 0 0 1 0 0  → 2 active bits (defensive core)
OR:       1 1 1 1 1 1 1 1  → 8 active bits (ALL ONES - dud!)
```

The AND of sword and shield gives you something minimal. Maybe a buckler. Small, shared essence of both.

The OR gives all ones. A dud code. Sword and shield have so little overlap that combining them fills every bit. You fused two complementary items and got nothing useful.

This is a real design lesson: items with very different bit patterns are dangerous to OR together.

</details>
