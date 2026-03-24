# Dave's Hash Map: A Guided Tour of Saying the Wrong Thing

_In which Dave Strider stores a sword and retrieves it by accident while talking to a bird._

---

## How Dave's Modus Works

Dave's sylladex uses a hash map. Every item gets a number. That number decides which card slot it goes in. The number comes from the item's name.

The formula:

```
1. Take the item name
2. Score each letter: vowels = 1, consonants = 2
3. Add up the total
4. Divide by the number of cards in the deck
5. The remainder is the slot number
```

That is it. That is the whole system. It sounds reasonable until you use it for thirty seconds.

---

## Storing the Ninja Sword

Dave picks up a ninja sword. Let us hash it.

**Item:** `ninja sword`

```
n = consonant = 2
i = vowel     = 1
n = consonant = 2
j = consonant = 2
a = vowel     = 1

s = consonant = 2
w = consonant = 2
o = vowel     = 1
r = consonant = 2
d = consonant = 2
```

**Spaces are ignored.** Total: `2+1+2+2+1+2+2+1+2+2 = 17`

Dave has 10 cards in his deck.

```
17 mod 10 = 7
```

The ninja sword goes in **slot 7**.

```
Slot: [0] [1] [2] [3] [4] [5] [6] [7]        [8] [9]
Item:                                  ninja sword
```

---

## The Retrieval Problem

Here is where it gets stupid. To retrieve an item, Dave does not just say "give me the ninja sword." He has to **say or think any word or phrase that hashes to the same slot number.**

The sylladex does not care about the content. It cares about the math.

---

## "stop" and the Bird Incident

Dave is on his roof. A bird is there. He says "stop."

Let us hash it.

**Word:** `stop`

```
s = consonant = 2
t = consonant = 2
o = vowel     = 1
p = consonant = 2
```

Total: `2+2+1+2 = 7`

```
7 mod 10 = 7
```

Slot 7. Where the ninja sword is.

```
HASH MATCH: "stop" → 7
ITEM IN SLOT 7: ninja sword
ACTION: EJECT ninja sword
```

Dave says "stop" to a bird and his ninja sword rockets out of his inventory.

This is not a bug. This is the system working exactly as designed. Two completely unrelated strings produced the same hash value. The map cannot tell the difference.

---

## The Collision Walkthrough

Let us put more items in Dave's deck and watch the chaos.

**Item:** `katana` (Dave would absolutely have a katana)

```
k=2, a=1, t=2, a=1, n=2, a=1 → total = 9
9 mod 10 = 9 → slot 9
```

**Item:** `shades`

```
s=2, h=2, a=1, d=2, e=1, s=2 → total = 10
10 mod 10 = 0 → slot 0
```

**Item:** `apple juice`

```
a=1, p=2, p=2, l=2, e=1,
j=2, u=1, i=1, c=2, e=1 → total = 15
15 mod 10 = 5 → slot 5
```

**Item:** `turntables`

```
t=2, u=1, r=2, n=2, t=2, a=1, b=2, l=2, e=1, s=2 → total = 17
17 mod 10 = 7 → slot 7
```

Slot 7. Where the ninja sword already is. **COLLISION.**

```
Slot: [0]     [1] [2] [3] [4] [5]          [6] [7]          [8] [9]
Item: shades                     apple juice     ninja sword          katana

INCOMING: turntables → slot 7

⚠️ COLLISION: slot 7 is occupied by ninja sword
```

If Dave's "detect collisions" checkbox is OFF: turntables overwrites ninja sword. The sword is gone. Ejected into the void. Dave now has turntables in slot 7 and a missing weapon.

If the checkbox is ON: turntables gets rejected. It does not enter the deck. Dave has to either clear the slot or increase his deck size to change the mod value.

---

## What Dave Might Say About This

> **TG: ok so my inventory system is basically a roulette wheel where the ball is a deadly weapon**
> **TG: every time i open my mouth theres a nonzero chance that a katana just fires out of my sylladex**
> **TG: i said the word "bro" to my bro and my shuriken hit the fridge**
> **TG: because apparently "bro" hashes to the same slot as "shuriken"**
> **TG: let me check that actually**
> **TG: b is 2 r is 2 o is 1 thats 5**
> **TG: shuriken is s2 h2 u1 r2 i1 k2 e1 n2 thats 13**
> **TG: 5 mod 10 is 5 and 13 mod 10 is 3**
> **TG: ok those dont actually collide i was being dramatic**
> **TG: but the POINT stands**
> **TG: this system turns every conversation into an accidental weapons discharge**
> **TG: hash maps are a menace to anyone who owns sharp objects**

---

## The Math of "How Likely Is a Collision?"

With 10 slots and items whose hash values range from small numbers (short names) to larger numbers (long names), collisions are inevitable. This is a version of the birthday problem:

> In a room of 23 people, there is a 50% chance two share a birthday (out of 365 possible days). With 10 slots and just 4 items, the chance of at least one collision is:

```
P(no collision with 4 items, 10 slots):
First item:  10/10 = 1.000
Second item:  9/10 = 0.900
Third item:   8/10 = 0.800
Fourth item:  7/10 = 0.700

P(no collision) = 1.0 × 0.9 × 0.8 × 0.7 = 0.504
P(at least one collision) = 1 - 0.504 = 0.496
```

**With just 4 items in 10 slots, there is already a 49.6% chance of a collision.** Dave's life is a coin flip every time he picks something up.

---

## Try It Yourself

Hash these words using Dave's system (vowels=1, consonants=2, mod 10) and figure out which ones collide:

1. `sword`
2. `words`
3. `birds`
4. `shirt`

<details>
<summary>Answers</summary>

```
sword: s2+w2+o1+r2+d2 = 9 → 9 mod 10 = 9
words: w2+o1+r2+d2+s2 = 9 → 9 mod 10 = 9   ← COLLISION with sword!
birds: b2+i1+r2+d2+s2 = 9 → 9 mod 10 = 9   ← TRIPLE COLLISION
shirt: s2+h2+i1+r2+t2 = 9 → 9 mod 10 = 9   ← FOUR-WAY COLLISION
```

Every single one hashes to 9. They all have the same vowel/consonant pattern: four consonants and one vowel. Any 5-letter word with exactly one vowel will hash to `(4×2)+(1×1) = 9`.

This is why Dave's hash function is terrible. It does not care about letter identity or position. It only counts vowels vs consonants. The entire English language's worth of 5-letter-one-vowel words all land in the same slot.

Real hash functions use the actual character values and their positions to minimize this. Dave's does not. Dave suffers.

</details>
