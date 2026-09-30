# HackMyVM - Venus

## Level 01 — Hidden File

### 🎯 Mission

User `sophia` has saved her password in a hidden file in the current directory.

**Goal:** Find the hidden file and log in as `sophia`.

---

### 🔎 Enumeration

First, I listed the files in the current directory:

```bash
ls
```

The directory contained:

```text
mission.txt
readme.txt
```

I then read the mission:

```bash
cat mission.txt
```

The mission indicated that Sophia's password was stored in a **hidden file**.

---

### 🕵️ Finding Hidden Files

To display hidden files, I used:

```bash
ls -alt
```

This revealed a suspicious hidden file:

```text
.myhiddenpazz
```

---

### 🔐 Retrieving the Password

I read the hidden file:

```bash
cat .myhiddenpazz
```

The file contained Sophia's password.

**Password:** `[REDACTED]`

---

### 👤 Logging in as Sophia

I used `su` to switch to the `sophia` user:

```bash
su sophia
```

After entering the discovered password, I successfully logged in as:

```text
sophia@venus
```

---

### ✅ Result

Successfully gained access to the `sophia` account.

**Flag:** `[REDACTED]`
**Password:** `[REDACTED]`
