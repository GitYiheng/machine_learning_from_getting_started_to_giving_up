# File Modes and Permissions

Every Unix file has a set of permissions that determine whether you can read, write, or run the file. Running `ls -l` displays the permissions:

```
-rw-r--r-- 1 user group 4096 Aug 14 12:24 unix_permissions.md
```

The file's mode `-rw-r--r--` represents the file's permissions and some extra information. There are four parts to the mode:

```
[type 1 bit][user permissions 3 bits][group permissions 3 bits][other permissions]
```

The first character of the mode is the file type. A dash `-` in this position denotes a regular file, meaning that there's nothing special about the file. Directories are also common and are indicated by a `d` in the file type slot.

The rest of a file's mode contains the permissions, which break down into three sets: user, group, and other, in that order. Each permission set can contain four basic representations:

- `r` means that the file is readable.
- `w` means that the file is writable.
- `x` means that the file is executable (you can run it as a program).
- `-` means nothing.

The user permissions pertain to the user who owns the file. Group permissions are for the file's group. Any user in that group can take advantage of these permissions. Everyone else on the system has access according to the other permissions.

Some executable files have an `s` in the user permissions listing instead of an `x`. This indicates that the executable is setuid, meaning that when you execute the program, it runs as though the file owner is the user instead of you.

# Modifying Permissions

To change permissions, use the `chmod` command.

```
chmod 644 file
```

| decimal | binary | permissions |
|:----------:|:-------------:|:------|
| 0 | 000 | none |
| 1 | 001 | executable |
| 2 | 010 | writable |
| 3 | 011 | writable, executable |
| 4 | 100 | readable |
| 5 | 101 | readable, executable |
| 6 | 110 | readable, writable |
| 7 | 111 | readable, writable, executable |


