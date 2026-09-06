# Undo

**Difficulty:** Easy     
**Category:** General

## Description

The challenge provides a transformed string and a hint at each step.

The goal is to identify the transformation that was applied and use the appropriate Linux command to undo it.

Each transformation must be reversed in the correct order.

---

## Step 1 — Base64

**Hint:**

> Base64 encoded the string.

The string was encoded using Base64.

To reverse the transformation:

```bash
base64 -d
```

---

## Step 2 — Reverse

**Hint:**

> Reversed the text.

The text was reversed, so we can use:

```bash
rev
```

---

## Step 3 — Dashes to Underscores

**Hint:**

> Replaced underscores with dashes.

The original underscores were replaced with dashes:

```text
_ → -
```

To reverse the transformation:

```bash
tr '-' '_'
```

The challenge did not allow `sed`, so `tr` was used instead.

---

## Step 4 — Parentheses to Curly Braces

**Hint:**

> Replaced curly braces with parentheses.

The transformation was:

```text
{ → (
} → )
```

To reverse it:

```bash
tr '()' '{}'
```

---

## Step 5 — ROT13

**Hint:**

> Applied ROT13 to letters.

ROT13 shifts each letter by 13 positions.

Since ROT13 is self-inverse, we can apply ROT13 again to recover the original text:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

## Solution Summary

The transformations were reversed in the following order:

```text
Base64 Decode
     ↓
Reverse
     ↓
- → _
     ↓
() → {}
     ↓
ROT13
```

### Commands Used

```bash
base64 -d
rev
tr '-' '_'
tr '()' '{}'
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

---

## Conclusion

This challenge was mainly about recognizing the transformation from each hint and applying the corresponding Linux command to reverse it.

The key concept is to undo the transformations in reverse order.

