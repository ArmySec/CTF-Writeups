# BYTEMANCY 1

**Category:** General Skills      
**Difficulty:** Easy

## Challenge Description


> Can you conjure the right bytes?

The challenge provides a Python source code file and a remote service that can be accessed using `nc`.

The service asks:

```text
Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.
```

## Solution

The key to solving this challenge is understanding what ASCII decimal `101` represents and how the Python source code checks the input.

### 1. Connect to the service

I connected to the remote service using:

```bash
nc foggy-cliff.picoctf.net 55381
```


The service displayed:

```text
Send me ASCII DECIMAL 101 1751 times, side-by-side, no space.
```


This indicates that we need to provide the ASCII character represented by decimal `101`, repeated `1751` times without spaces.

### 2. Inspect the source code

The challenge provides the Python source code.

The important part is:

```python
user_input = input('==> ')

if user_input == "\x65"*1751:
    print(open("./flag.txt", "r").read())
    break
```


The comparison tells us exactly what input the program expects.

### 3. Understand ASCII decimal 101

ASCII decimal `101` represents the character:

```text
e
```

The source code uses:

```python
\x65
```

which is the hexadecimal representation of decimal `101`.

Therefore:

```python
\x65
```

is equivalent to:

```text
e
```


### 4. Understand the required input

The condition is:

```python
"\x65"*1751
```

Since `\x65` represents `e`, the program expects:

```text
e
```

repeated **1751 times**, with no spaces.

Manually entering 1751 characters would be unnecessary, so I generated the required input using Python.

### 5. Generate the required input

I used the following command:

```bash
python3 -c "print('e' * 1751)"
```


This generates the character `e` exactly 1751 times.

### 6. Send the input to the server

Instead of copying the generated string manually, I piped it directly into `nc`:

```bash
python3 -c "print('e' * 1751)" | nc foggy-cliff.picoctf.net 55381
```

The generated input matches the condition:

```python
user_input == "\x65"*1751
```

The server accepts the input and reveals the flag.

### 7. Read the result

After sending the correct input, the program reaches:

```python
print(open("./flag.txt", "r").read())
```


This causes the challenge to display the flag.

## Key Takeaway

The main trick in this challenge is recognizing that ASCII decimal `101` represents the character `e`.

The source code makes the expected input explicit:

```python
"\x65"*1751
```

Since `\x65` is hexadecimal `65`, which corresponds to decimal `101`, the required input is simply the character `e` repeated **1751 times**.

Using Python allows us to generate and send the input efficiently:

```bash
python3 -c "print('e' * 1751)" | nc foggy-cliff.picoctf.net 55381
```

## Flag

The flag is intentionally omitted from this write-up.
