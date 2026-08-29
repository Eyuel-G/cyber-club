# Linux File Management Practice

**Author:** Eyuel Getachew  
**Environment:** Kali Linux Terminal  

---

## Introduction

In this lab, I practiced basic Linux commands for working with files and directories in the Kali Linux terminal. I created a few files, added text to them, renamed one, copied a file, and cleaned up some files and a directory.

The main commands I practiced were `cd`, `mkdir`, `touch`, `ls`, `echo`, `mv`, `cp`, `rm`, and `cat`.

---

## Lab Execution

### 1. Creating the Working Directory

I started by navigating to the Desktop and creating a directory named `linux_test` to work in:

```bash
cd Desktop
mkdir linux_test
cd linux_test
```

Now I was working inside `~/Desktop/linux_test/`.

---

### 2. Creating Text Files

Inside `linux_test`, I created three text files at the same time using `touch`:

```bash
touch one.txt two.txt three.txt
```

I checked the directory contents with `ls`:

```bash
ls
```

**Output:**
```text
one.txt  three.txt  two.txt
```

All three files were empty at this point.

---

### 3. Adding Text to Files

I used `echo` with the `>` operator to write a line of text into each file:

```bash
echo "This is text for the first file" > one.txt
echo "This is text for the second file" > two.txt
echo "This is text for the third file" > three.txt
```

The `>` operator redirects the output of `echo` into the file instead of printing it to the terminal screen.

For example, checking `one.txt` showed:
```text
This is text for the first file
```

---

### 4. Renaming a File

Next, I renamed `three.txt` to `final.txt` using `mv`:

```bash
mv three.txt final.txt
```

The `mv` command is used for both moving and renaming files. The file was renamed to `final.txt`, but its contents stayed the same.

---

### 5. Creating Another Directory & Copying Files

I went back up to the Desktop and created another directory called `new_directory`:

```bash
cd ..
mkdir new_directory
cd linux_test/
```

I checked the files inside `linux_test` again:

```bash
ls
```

**Output:**
```text
final.txt  one.txt  two.txt
```

#### Copying `one.txt`
I practiced copying `one.txt` into `new_directory` using both a relative path and an absolute path:

```bash
# Relative path
cp one.txt new_directory

# Absolute path (~ represents home directory)
cp one.txt ~/Desktop/new_directory
```

The `cp` command makes a copy of the file at the destination while leaving the original file in place.

---

### 6. Removing Directories and Files

I removed `new_directory` using `rm -rf`:

```bash
rm -rf new_directory
```

I checked with `ls` and confirmed the directory was gone.

> **Note:** `rm -rf` removes directories and everything inside them without asking for confirmation, so it needs to be used carefully.

Next, I deleted `two.txt`:

```bash
rm -rf two.txt
```

Checking the directory again:

```bash
ls
```

**Output:**
```text
final.txt  one.txt
```

For a normal file, `rm two.txt` would have been enough, but I used `rm -rf` during practice to get comfortable with the flags.

---

### 7. Checking File Contents

Finally, I used `cat` to check the contents of the remaining files.

For `final.txt`:
```bash
cat final.txt
```

**Output:**
```text
This is text for the third file
```

For `one.txt`:
```bash
cat one.txt
```

**Output:**
```text
This is text for the first file
```

---

## Final Directory Structure

```text
linux_test/
├── final.txt
└── one.txt
```

---

## Commands Summary

| Command | Usage Example | Purpose |
| :--- | :--- | :--- |
| `cd` | `cd Desktop` | Change directory |
| `mkdir` | `mkdir linux_test` | Create a directory |
| `touch` | `touch one.txt two.txt` | Create empty files |
| `ls` | `ls` | List directory contents |
| `echo` | `echo "text" > file.txt` | Write text into a file |
| `mv` | `mv three.txt final.txt` | Rename or move files |
| `cp` | `cp file.txt path/` | Copy files |
| `rm` | `rm two.txt` | Delete a file |
| `rm -rf` | `rm -rf directory_name` | Remove directory and its contents |
| `cat` | `cat final.txt` | Display file contents |

---

## Conclusion

This was a basic Linux file management exercise, but it gave me good hands-on practice in the Kali Linux terminal. I got to work with creating files and directories, writing to files, renaming, copying, and deleting them.

One important takeaway is to be careful with `rm -rf` since CLI deletions are permanent. Overall, this was solid practice for getting more comfortable using the Linux command line instead of doing everything through a desktop interface.
