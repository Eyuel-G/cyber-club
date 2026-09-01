# Linux Users and Groups Practice

**Author:** Eyuel Getachew  
**Environment:** Kali Linux Terminal  

---

## Introduction

In here, I practiced Linux user account and group management in the Kali Linux terminal. I created a new user account with a home directory, created a custom group, assigned supplementary group permissions, switched user contexts, and evaluated default file ownership rules upon file creation.

The main commands practiced during this session were `whoami`, `cut`, `useradd`, `groupadd`, `usermod`, `groups`, `id`, `su`, `pwd`, `touch`, and `ls -l`.

---

## Practice Steps

### 1. Checking the Current User

I began by verifying the active logged-in user:

```bash
whoami
```

**Output:**
```text
eyuel_g
```

This confirmed I was operating under my primary user account, `eyuel_g`.

---

### 2. Creating the Test User

First, I inspected existing system users by parsing `/etc/passwd`:

```bash
cut -d: -f1 /etc/passwd
```

Next, I created a new user account named `student1`. I included the `-m` flag to automatically create a home directory (`/home/student1`):

```bash
sudo useradd -m student1
```

I re-checked the system accounts list:

```bash
cut -d: -f1 /etc/passwd
```

**Output snippet:**
```text
eyuel_g
testuser
student1
```

The output confirmed that `student1` was successfully added to the system.

---

### 3. Creating the `developers` Group

Before assigning custom permissions, I listed the existing system groups:

```bash
cut -d: -f1 /etc/group
```

I then created a new group named `developers`:

```bash
sudo groupadd developers
```

The group `developers` was created successfully.

---

### 4. Adding `student1` to the `developers` Group

To grant secondary group memberships without overriding existing groups, I used `usermod` with `-aG` (append to group):

```bash
sudo usermod -aG developers student1
```

I verified the updated group assignment:

```bash
groups student1
```

**Output:**
```text
student1 : student1 developers
```

I also checked detailed account identification data using `id`:

```bash
id student1
```

**Output:**
```text
uid=1002(student1) gid=1002(student1) groups=1002(student1),1003(developers)
```

**Analysis:**
- **UID (User ID):** `1002` (`student1`)
- **GID (Primary Group ID):** `1002` (`student1`)
- **Supplementary Groups:** `1002(student1)`, `1003(developers)`

This confirmed `student1` retained `student1` as its primary group while successfully joining `developers` as a supplementary group.

---

### 5. Switching User Context

Next, I switched context to the `student1` account using a login shell (`su -`):

```bash
su - student1
```

I verified the active session user identity:

```bash
whoami
```

**Output:**
```text
student1
```

I confirmed the current working directory:

```bash
pwd
```

**Output:**
```text
/home/student1
```

Finally, I checked active group privileges inside the new session:

```bash
groups
```

**Output:**
```text
student1 developers
```

---

### 6. Creating a File as `student1`

While logged in as `student1`, I created a new test file in its home directory:

```bash
touch student_file.txt
```

I inspected the detailed file attributes using `ls -l`:

```bash
ls -l student_file.txt
```

**Output:**
```text
-rw-rw-r-- 1 student1 student1 0 Sep 1 09:04 student_file.txt
```

---

### 7. Analyzing Default File Ownership Rules

From the directory listing:

```text
-rw-rw-r-- 1 student1 student1 0 Sep 1 09:04 student_file.txt
```

- **Owner:** `student1`  
  Because the file was created by the active user `student1`.
- **Group:** `student1`  
  Linux automatically assigns the user's **primary group** (`student1`) as the default group owner for newly created files.
- **Supplementary Group Behavior:**  
  Even though `student1` belongs to the `developers` group, secondary/supplementary groups are not automatically assigned to new files upon creation unless explicit group inheritance rules (such as `SGID` on directories) or `chown` modifications are applied.

---

## Final Result & Summary

### Account & Group Setup Summary

| Entity | Identity | Type | Value |
| :--- | :--- | :--- | :--- |
| **User** | `student1` | User Account | UID `1002` |
| **Primary Group** | `student1` | Primary Group | GID `1002` |
| **Secondary Group** | `developers` | Supplementary Group | GID `1003` |
| **Home Directory** | `/home/student1` | System Directory | `drwxr-xr-x` |

### Created File Ownership Breakdown

| Attribute | Value | Explanation |
| :--- | :--- | :--- |
| **File Name** | `student_file.txt` | Target test file created |
| **Permissions** | `-rw-rw-r--` | Read/Write for owner & group, Read-only for others |
| **File Owner** | `student1` | Inherited from creating user account |
| **Group Owner** | `student1` | Inherited from user's primary group |

---

## Commands Summary

| Command | Usage Example | Purpose |
| :--- | :--- | :--- |
| `whoami` | `whoami` | Display active logged-in user |
| `cut` | `cut -d: -f1 /etc/passwd` | Parse system account usernames from database |
| `useradd` | `sudo useradd -m student1` | Create user account with home directory (`-m`) |
| `groupadd` | `sudo groupadd developers` | Create a new user group |
| `usermod` | `sudo usermod -aG developers student1` | Append supplementary group membership (`-aG`) |
| `groups` | `groups student1` | List group memberships for a user |
| `id` | `id student1` | Display detailed UID, GID, and group associations |
| `su` | `su - student1` | Switch to another user with complete environment load |
| `pwd` | `pwd` | Print working directory path |
| `touch` | `touch student_file.txt` | Create an empty file |
| `ls -l` | `ls -l student_file.txt` | Display permissions, owner, and group metadata |

---

## Conclusion

This session provided practical experience with Linux user accounts, group management, user switching, and default file permissions. I gained a practical understanding of how primary vs. secondary groups operate in Linux, how context switching with `su -` alters the environment, and how default file creation assigns ownership based on the active user and primary group.



<img width="500" height="500" alt="users_1" src="https://github.com/user-attachments/assets/65245b39-3177-41d6-8f0d-dcdcfcf73017" />
<img width="500" height="500" alt="users_2" src="https://github.com/user-attachments/assets/8495ada7-dbdd-4a44-a5d3-3c8e71d5e5a4" />
<img width="500" height="500" alt="users_3" src="https://github.com/user-attachments/assets/f940d37a-b214-410d-a67a-d712c93eaf1b" />
<img width="500" height="500" alt="users_4" src="https://github.com/user-attachments/assets/68909583-84cc-4882-b94c-d93677065c19" />
<img width="500" height="500" alt="users_5" src="https://github.com/user-attachments/assets/ba0d4dbf-8396-403e-b1a0-faba6662900a" />




