# Linux File Permissions and Ownership Practice

**Author:** Eyuel Getachew  
**Environment:** Kali Linux Terminal  

---

## Introduction

In this lab, I practiced Linux file permissions and ownership management in the Kali Linux terminal. I created a file, modified its permission flags using octal notation, created a dedicated user and group, and transferred file ownership.

The main commands I practiced were `chmod`, `ls -l`, `groupadd`, `useradd`, `passwd`, `cut`, and `chown`.

---

## Lab Execution

### 1. Creating the Test File

I started by navigating to the `linux_test` directory located on the Desktop:

```bash
cd Desktop
cd linux_test
```

My current location was `~/Desktop/linux_test`.

I then created a new file named `secret.txt`:

```bash
touch secret.txt
```

I checked the contents of the directory using `ls`:

```bash
ls
```

**Output:**
```text
final.txt  one.txt  secret.txt
```

`secret.txt` was successfully created.

---

### 2. Setting File Permissions

Next, I updated the permissions of `secret.txt` using `chmod`:

```bash
chmod 640 secret.txt
```

The `chmod` command is used to change the permissions of a file.

The octal value `640` breaks down as follows:
- **6** → Owner permissions (`4 + 2 = 6`: read + write)
- **4** → Group permissions (`4`: read only)
- **0** → Others permissions (`0`: no access)

Permission value key:
- **4** = Read (`r`)
- **2** = Write (`w`)
- **1** = Execute (`x`)

Therefore:
- **Owner (`eyuel_g`):** Read and write access (`rw-`)
- **Group (`eyuel_g`):** Read-only access (`r--`)
- **Others:** No access (`---`)

I verified the permissions with `ls -l`:

```bash
ls -l secret.txt
```

**Output:**
```text
-rw-r----- 1 eyuel_g eyuel_g 0 Aug 30 23:27 secret.txt
```

At this stage, both the owner and group were set to `eyuel_g`.

---

### 3. Creating a Test User and Group

To test group and ownership permissions properly, I created a new group and user.

First, I created a new group named `testgroup`:

```bash
sudo groupadd testgroup
```

Next, I created a new user `testuser` and assigned `testgroup` as its primary group:

```bash
sudo useradd -m -g testgroup testuser
```

I then set a password for `testuser`:

```bash
sudo passwd testuser
```

To confirm the user was added to the system, I listed system usernames using `cut`:

```bash
cut -d: -f1 /etc/passwd
```

At the bottom of the output, both users were present:

```text
eyuel_g
testuser
```

This confirmed `testuser` was successfully created.

---

### 4. Changing File Ownership

Back inside the `linux_test` directory, I transferred ownership of `secret.txt` to the new user and group using `chown`:

```bash
sudo chown testuser:testgroup secret.txt
```

The `chown` command uses the syntax `chown owner:group filename`.

I checked the updated ownership details with `ls -l`:

```bash
ls -l secret.txt
```

**Output:**
```text
-rw-r----- 1 testuser testgroup 0 Aug 30 23:27 secret.txt
```

The ownership changed from `eyuel_g eyuel_g` to `testuser testgroup`, while retaining the `640` permissions.

---

## Final Result & Permission Summary

```text
-rw-r----- 1 testuser testgroup 0 Aug 30 23:27 secret.txt
```

| Scope | Subject | Permission String | Numeric Code | Access Granted |
| :--- | :--- | :--- | :--- | :--- |
| **Owner** | `testuser` | `rw-` | `6` | Read + Write |
| **Group** | `testgroup` | `r--` | `4` | Read Only |
| **Others** | Everyone else | `---` | `0` | No Access |

---

## Commands Summary

| Command | Usage Example | Purpose |
| :--- | :--- | :--- |
| `touch` | `touch secret.txt` | Create an empty file |
| `chmod` | `chmod 640 secret.txt` | Change file permissions |
| `ls -l` | `ls -l secret.txt` | Display detailed file info & permissions |
| `groupadd` | `sudo groupadd testgroup` | Create a new user group |
| `useradd` | `sudo useradd -m -g testgroup testuser` | Create a new user and set primary group |
| `passwd` | `sudo passwd testuser` | Set or change a user's password |
| `cut` | `cut -d: -f1 /etc/passwd` | Extract specific fields from text file output |
| `chown` | `sudo chown testuser:testgroup secret.txt` | Change file owner and group |

---

## Conclusion

This session provided practical experience with Linux file permissions, user account management, and ownership assignment. I learned how to use octal notation (`640`) with `chmod` to specify read/write access for owners, groups, and others, as well as how to create new system users/groups and reassign file ownership using `chown`.
