# Understanding the role of ownership

- Each user is member of one primary group and optionally member of secondary groups
- Most Linux distributions use **private groups**, which means that while creating a user, a group with the name of the user is created and the user is the only member of the group
- Each file has a user owner and a group owner
- When a user creates a file, that user is the file owner and the user's primary group is the group owner of the new file
- Primary group is used for group owner, secondary groups are primarily used to assign additional permissions to the user

# Creating users with adduser

- Use `useradd <username>` to create an user
- **On Ubuntu: use `useradd -m` to ensure the user has a home directory**
- When a user is created, then the default settings from file `/etc/login.defs` are applied
- Use `useradd -D` to list the default settings when adding users
- Users are registered in file `/etc/passwd`
- When a new user is added, the password is locked. Let the user generate a SSH keypair and append the public key to `/home/username/.ssh/authorized_keys`. Then the user uses SSH to login (without password) and can set his password with `sudo passwd` (might be required when user needs `sudo` to execute system commands).

```
sudo useradd jan
sudo userdel -rf jan
```

# Creating groups with groupadd

- Use `groupadd <groupname>` to create a group
- Use `usermod -aG <groupname> <username>` to add user to secondary group
- Groups are registered in file `/etc/group`

# Managing user and group properties

The `/etc/passwd` file is a plain text (ASCII), colon-separated (:) system file (owned by root, usually mode 644) that stores essential user account information. Each line represents a user with seven fields:

1. **Username:** Login name (1–32 characters).
2. **Password (x):** An x or \* indicates that the actual password hash is in `/etc/shadow`.
3. **User ID (UID):** Unique numerical ID (e.g., 0 for root, 1-999 for system/predefined accounts).
4. **Group ID (GID):** Primary group ID.
5. **User Info (GECOS):** Optional field for full name, office, or phone number.
6. **Home Directory:** Absolute path to the user's home folder.
7. **Shell:** The default shell (e.g., `/bin/bash` or `/sbin/nologin`).

- Use `getent passwd <username>` to list the user properties in `/etc/passwd`
- Password properties, including the pasword hash, are stored in `/etc/shadow`
- Use command `vipw` to edit `/etc/passwd` or `/etc/shadow` directly (**Recommended not use this command**)
- Use `usermod` to modify user settings
- Use `useradd` to delete user
- Likewise there is `groupadd`, `groupmod` and `groupdel`
- Use `id` to list information about user accounts

The `/etc/group` file is a plain text (ASCII), colon-separated (:) system file (owned by root, usually mode 644) that stores essential group information. Each line represents a group with 4 fields:

1. **Group Name**
2. **Group Password (x):** Often encrypted, but usually marked with an x (or !), indicating the actual password hash is stored in `/etc/gshadow`.
3. **Group ID (GID)**
4. **Group Membership List:** A comma-separated list of usernames belonging to this group. It does not contain spaces between user names.

- Group Password hashes are stored in `/etc/gshadow` (not used anymore)
- Use command `vigr` to edit `/etc/group`directly (**Recommendation: Do not use this command**)

# Configuring defaults for new users

- Use `useradd -D` to list the default settings when adding users
- When a new user is created, then the default settings from file `/etc/login.defs` are applied. For example the password aging controls can be configured here.
- When a new user is created, then the files in directory `/etc/skel` are copied to user's home directory

# Managing password properties

- Password properties, including the pasword hash, are stored in `/etc/shadow`
- Use `passwd` or `sudo passwd <username>` to change your password or from another user
- Use `passwd -S` or `sudo passwd -S <username>` to list your password properties or from another user
- Use `chage` or `sudo chage <username>` to change your password properties or from another user in an interative way
- Change password properties without interactive prompt

```
(Redhat) echo "password" | sudo passwd --stdin username
(Ubuntu) echo "username:password" | sudo chpasswd
```

# Managing current sessions

- Who is doing what on the system?
- Use `who` or `w` (for a bit more detail) to list users are currently logged in.
- Use `loginctl` for current session management

```
loginctl list-sessions
loginctl show-session <session-id>
loginctl show-user <username>
loginctl terminate-session <session-id>
```
