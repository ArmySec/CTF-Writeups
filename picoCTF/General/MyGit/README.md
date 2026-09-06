# MY GIT

**Category:** General Skills       
**Difficulty:** Easy

## Challenge Description

> I have built my own Git server with my own rules!

## Solution

The challenge provides a custom Git server with a specific rule for updating `flag.txt`.

### 1. Clone the repository

First, I cloned the repository provided by the challenge:

```bash
git clone ssh://git@foggy-cliff.picoctf.net:60777/git/challenge.git
cd challenge
```

### 2. Inspect the repository

I checked the repository status, branches, commits, and remote:

```bash
git status
git log --oneline --all
git branch -a
git remote -v
```

The most important clue was in the `README.md`:

```text
Only flag.txt pushed by root:root@picoctf will be updated with the flag.
```

This tells us that the server checks the Git identity associated with the commit.

The required identity is:

```text
Username: root
Email: root@picoctf
```

### 3. Create `flag.txt`

I created a temporary `flag.txt` file:

```bash
echo "test" > flag.txt
```

The content itself is not important. The server will replace it with the flag after a valid push.

### 4. Configure the Git identity

Next, I configured Git to use the required username and email:

```bash
git config user.name "root"
git config user.email "root@picoctf"
```

### 5. Commit the file

I added the file and created a commit:

```bash
git add flag.txt
git commit -m "update flag"
```

To verify the commit identity, I ran:

```bash
git log -1 --format=full
```

The commit showed:

```text
Author: root <root@picoctf>
Commit: root <root@picoctf>
```

This confirmed that the commit was created using the required identity.

### 6. Push the commit

Finally, I pushed the commit to the challenge server:

```bash
git push origin master
```

The server recognized the commit because it was created by:

```text
root <root@picoctf>
```

It then updated `flag.txt` with the actual flag.

### 7. Read the flag

I displayed the updated file with:

```bash
cat flag.txt
```

The flag was successfully revealed.

## Key Takeaway

The main trick in this challenge is understanding that the custom Git server uses the **author identity of the commit** as part of its rules.

By configuring:

```text
user.name = root
user.email = root@picoctf
```

and pushing the commit to the challenge server, the server updates `flag.txt` with the flag.

## Flag

```text
FLAG_GOES_HERE
```
