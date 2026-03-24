# Captchalogue Codes: The Math

Every item in Homestuck has an 8-character code. This is the system that makes alchemy possible. The code identifies the item, and operations on the code produce new item codes.

This doc is about the math of the code system itself.

---

## The Code Space

Each of the 8 characters in a code can be one of 64 values:
- Lowercase a-z: 26
- Uppercase A-Z: 26
- Digits 0-9: 10
- Special characters `!` and `?`: 2

Total: 26 + 26 + 10 + 2 = 64

The number of possible unique 8-character codes is:

64^8 = 281,474,976,710,656

That is roughly 281 trillion possible items.

---

## Why 64 Per Character

64 = 2^6. Each character is a 6-bit value. Eight characters at 6 bits each = 48 bits total per code. This is why bitwise operations work cleanly on these codes. You are operating on a 48-bit number, just displayed in a human-readable base-64 format instead of as a string of 1s and 0s.

---

## The Dud Problem

Not every one of those 281 trillion codes corresponds to a real item. Many produce nothing. These are called junk codes or dud codes.

AND operations always reduce the number of active bits in the result (or keep them the same). Repeated AND-ing of codes pushes the result toward `00000000`: a code of all zeros, which is a dud.

OR operations always increase the number of active bits. Repeated OR-ing pushes the result toward `!!!!!!!!`: a code of all 1s (since `!` is the highest value in the character set), which is also a dud.

The practical result is that the more you chain combinations together, the closer you get to a garbage code. This explains why John's increasingly absurd item combinations (jetpack fused with a cinderblock fused with a violin) produce abominations instead of useful equipment.

---

## Finite Items in an Infinite Universe

The comic raises the issue directly through John. There are infinite universes, and codes are transferable across sessions. But the total code space is 281 trillion. At some point, across all sessions in all universes, every possible code gets used.

This is a real CS problem called address space exhaustion. IPv4 addresses (32-bit) ran out. IPv6 (128-bit) was created to buy more time. The captchalogue code system is running a 48-bit address space with no upgrade path.

---

## Worked Examples

> **See it in action:** [The Code Space Expedition: 281 Trillion Items and Counting](examples/04a_code_space_expedition.md) — How long it takes to exhaust the code space, the birthday problem applied to code collisions, exact decay math for AND and OR chains, a full base-64 encoding breakdown, and the all-zeros/all-ones dud wall problem.
