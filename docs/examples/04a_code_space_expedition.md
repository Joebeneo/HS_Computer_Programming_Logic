# The Code Space Expedition: 281 Trillion Items and Counting

_In which we do the math on Homestuck's item code system and discover exactly how big, how small, and how doomed it is._

---

## How Big Is 281 Trillion?

The captchalogue code system has 64^8 = 281,474,976,710,656 possible codes.

That number is abstract. Let us make it less abstract.

**If you created one new item per second:**
```
281,474,976,710,656 seconds
÷ 60                         = 4,691,249,611,844 minutes
÷ 60                         = 78,187,493,530 hours
÷ 24                         = 3,257,812,230 days
÷ 365.25                     = 8,919,876 years

That is roughly 8.9 million years to use every code.
```

For reference, 8.9 million years ago, the common ancestor of humans and chimpanzees was still walking around. You would need to start alchemy before our species existed to fill the code space by now.

**If every human on Earth (8 billion) each created one item per second simultaneously:**
```
8,919,876 years ÷ 8,000,000,000 people ≈ 0.001 years ≈ 9.7 hours
```

Eight billion people working together could exhaust the code space in under 10 hours. Suddenly 281 trillion does not feel as big.

---

## The 48-Bit Reality

Each code is 48 bits. Here is how that stacks up against other addressing systems:

| System | Bits | Possible Values | Exhausted? |
|--------|------|----------------|------------|
| IPv4 addresses | 32 | 4.3 billion | Yes. Ran out around 2011 |
| Captchalogue codes | 48 | 281 trillion | Depends on how many universes |
| MAC addresses | 48 | 281 trillion | Same size as captchalogue codes |
| IPv6 addresses | 128 | 340 undecillion | Not in our lifetimes |
| SHA-256 hash | 256 | More than atoms in the universe | Effectively never |

Captchalogue codes have the same address space as MAC addresses (the unique IDs on network cards). We have been assigning MAC addresses since the 1980s and have used a small fraction of the space. But we are one planet. Homestuck has infinite universes, each running Sburb sessions, each generating items.

---

## The Collision Guarantee

Here is a fun one. How many items need to exist before a code collision (two different items with the same code) becomes more likely than not?

This is the birthday problem again. The formula:

```
P(collision) ≈ 1 - e^(-n² / (2 × total_codes))
```

Solving for P = 0.50:

```
n ≈ √(2 × 281,474,976,710,656 × ln(2))
n ≈ √(390,180,644,391,481)
n ≈ 19,753,244
```

**After about 19.75 million items, there is a 50% chance that two items share a code.**

That sounds like a lot until you remember that every Sburb session across every universe is generating items. If each session produces a few hundred items and there are millions of sessions, you hit 19 million items fast. And once you have a collision, two different items have the same code. Alchemy stops being deterministic.

---

## The Decay Math

We showed in the alchemy workshop that AND and OR chains decay toward duds. Here is the math on how fast.

**AND decay:**

If each code has, on average, 50% of its bits active (24 out of 48), then AND-ing two random codes produces a result with about 25% active bits. AND-ing three: about 12.5%. The formula:

```
Expected active bits after k AND operations = 48 × (0.5)^k

k=1: 24 bits   (50%)
k=2: 12 bits   (25%)
k=3: 6 bits    (12.5%)
k=4: 3 bits    (6.25%)
k=5: 1.5 bits  (3.1%)
k=6: 0.75 bits (1.6%)
```

By 6 AND operations deep, you probably have 0 or 1 active bits. You are almost certainly at a dud.

**OR decay:**

Mirror image. OR-ing two 50%-active codes gives 75% active. Three: 87.5%.

```
Expected active bits after k OR operations = 48 × (1 - (0.5)^k)

k=1: 24 bits  (50%)
k=2: 36 bits  (75%)
k=3: 42 bits  (87.5%)
k=4: 45 bits  (93.75%)
k=5: 46.5     (96.9%)
k=6: 47.25    (98.4%)
```

By 6 OR operations, nearly all 48 bits are active. You are approaching `!!!!!!!!`.

**The window of useful alchemy is narrow.** Two to three combinations deep. After that, the math works against you.

---

## John's Discovery

The comic addresses this through John, who asks a version of: if there are infinite universes but only 281 trillion codes, what happens?

The answer is address space exhaustion. The same problem that killed IPv4.

When IPv4's 4.3 billion addresses ran out, the solution was IPv6 with 128 bits (a space so large it could assign an IP to every grain of sand on Earth and still have room). The captchalogue system has no equivalent upgrade. 48 bits is all you get.

Some implications the comic leaves for you to figure out:

1. **Duplicate items are guaranteed.** Across infinite sessions, every code is used infinite times. Separate items in separate universes can share a code.

2. **Alchemy results are universal.** If code `AbCdEfGh` produces a specific item in one session, it produces the same item in every session. The code space is shared.

3. **The "best" items are probably already known.** With a finite code space and infinite sessions, every useful combination has been discovered by someone. Nothing new is being created. Only rediscovered.

---

## Base-64 Encoding Breakdown

Each character in a code represents a 6-bit value. The mapping:

```
Character → Value (decimal) → Value (binary)

a =  0  = 000000        A = 26 = 011010
b =  1  = 000001        B = 27 = 011011
c =  2  = 000010        C = 28 = 011100
...                     ...
z = 25  = 011001        Z = 51 = 110011

0 = 52 = 110100
1 = 53 = 110101
...
9 = 61 = 111101

! = 62 = 111110
? = 63 = 111111
```

**Example code: `Da1?bZ0!`**

```
D = 29 = 011101
a =  0 = 000000
1 = 53 = 110101
? = 63 = 111111
b =  1 = 000001
Z = 51 = 110011
0 = 52 = 110100
! = 62 = 111110
```

Full 48-bit representation:
```
011101 000000 110101 111111 000001 110011 110100 111110
```

That is the item's true identity. The 8-character code is just a human-readable label for this binary number. All alchemy operates on the binary level.

---

## The All-Zeros and All-Ones Problem

**`00000000` (all a's in the character set) = 48 zero-bits**

AND anything with this code and you get all zeros back. It is the AND identity trap. In real math, this is like multiplying by zero. Everything becomes zero.

**`????????` (all ?'s) = 48 one-bits**

OR anything with this code and you get all ones back. It is the OR saturation ceiling. In real math, this is like adding infinity. Everything becomes infinity.

Both are duds. They sit at opposite ends of the code space like walls. Every AND chain slides toward one wall. Every OR chain slides toward the other.

---

## Try It Yourself

An item has the code `aaaa????`. That means the first 24 bits are all 0 and the last 24 bits are all 1.

```
000000 000000 000000 000000 111111 111111 111111 111111
```

Another item has the code `????aaaa`. First 24 bits all 1, last 24 bits all 0.

```
111111 111111 111111 111111 000000 000000 000000 000000
```

What is the AND? What is the OR?

<details>
<summary>Answer</summary>

**AND:**
```
000000 000000 000000 000000 111111 111111 111111 111111
111111 111111 111111 111111 000000 000000 000000 000000
──────────────────────────────────────────────────────
000000 000000 000000 000000 000000 000000 000000 000000
```
AND result: `aaaaaaaa` (all zeros). **Dud.** These two items have zero overlap.

**OR:**
```
000000 000000 000000 000000 111111 111111 111111 111111
111111 111111 111111 111111 000000 000000 000000 000000
──────────────────────────────────────────────────────
111111 111111 111111 111111 111111 111111 111111 111111
```
OR result: `????????` (all ones). **Also a dud.** Together they fill every bit.

Two perfectly complementary items cannot be combined by AND or OR. Both operations produce duds. This is the worst-case scenario for alchemy: two items that are total opposites at the bit level.

</details>
