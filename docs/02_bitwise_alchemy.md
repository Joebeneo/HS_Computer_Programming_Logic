# Bitwise Logic: Alchemy

Alchemy in Homestuck lets players combine items to create new ones. You take two captchalogue cards, interact with them in a specific way, and the resulting code determines what gets created.

The two methods are shown in the comic as:

- Overlapping two cards on top of each other (AND)
- Punching one card with both items' hole patterns (OR)

These are not just flavor. These are bitwise operations.

---

## What a Captchalogue Code Actually Is

Every item in Homestuck has an 8-character code on the back of its captchalogue card. Each character can be one of 64 things: lowercase letters (26), uppercase letters (26), digits 0-9 (10), and the special characters `!` and `?` (2). That gives 64 possible values per character slot.

Think of each character as a 6-bit number. 2^6 = 64. Eight of those side by side = 48 bits total.

When you combine two cards, you are doing a bitwise operation on those 48 bits.

---

## AND ( && )

**What it does:** Compares each bit in two codes. The result is 1 only if BOTH input bits are 1. Otherwise the result is 0.

**How it works in the comic:** Overlapping the cards physically obscures some of the punched holes. Only holes that are punched through on BOTH cards remain open. The resulting hole pattern is the AND of both codes.

**Concrete example:**
Code A: `10110`
Code B: `11010`
A AND B: `10010`

Only the positions where both had a 1 come through. Everything else goes dark. The resulting item is shaped by what both items had in common, in terms of their bit values.

**In practice:** AND tends to produce codes with fewer active bits. The result leans toward the item that "gave less" in the combination. This is why AND combinations often produce a version of one item with traits of the other stripped back in.

---

## OR ( || )

**What it does:** Compares each bit in two codes. The result is 1 if EITHER input bit is 1.

**How it works in the comic:** Punching one card with both hole patterns adds all the holes from both items onto a single card. Any hole from either card is present in the final card.

**Concrete example:**
Code A: `10110`
Code B: `11010`
A OR B: `11110`

Everything from both inputs survives. Nothing gets filtered out. The result is more "full" than either input on its own.

**In practice:** OR tends to produce codes with more active bits. The result is closer to a fusion where both items are represented. More chaotic combinations come from OR because you are throwing everything in together.

---

## Why This Matters Beyond the Comic

AND and OR are the two most basic logic gates in digital electronics and programming. Every conditional in every program you have ever run boils down to some variation of these. The fact that Homestuck uses them as the literal mechanic for combining objects is a very deliberate design choice. You are not just merging two things. You are performing logic on their binary representations to produce a new value.

---

## Worked Examples

> **See it in action:** [The Alchemy Workshop: Bitwise Fusion in Practice](examples/02a_alchemy_workshop.md) — Full worked examples of AND and OR on 8-bit codes, the AND decay chain and OR saturation problem with exact math, visual punch-card demonstrations, and why chaining more than 2-3 combinations deep produces guaranteed duds.
