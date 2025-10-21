# Ansible Module Command Examples

This is a collection of common Ansible module commands for managing remote servers. These examples cover file/directory operations, user/group management, and file transfers.

## 📝 Prerequisites

1.  **Ansible Inventory**: You must have an inventory file (e.g., `/etc/ansible/hosts`) configured with a group named `dev`.
2.  **Passlib**: For creating users with hashed passwords, the `passlib` library is required on the Ansible control node.
    ```bash
    sudo apt update
    sudo apt install python3-passlib
    ```

---

## 📂 File & Directory Management

These commands use the `shell` module to perform basic file and directory tasks.

### File Operations

```bash
# 1. Create a blank file named sample.txt
ansible dev -b -m shell -a "touch sample.txt"

# 2. List files to verify creation
ansible dev -b -m shell -a "ls -l"

# 3. Change file permissions to read-only for the owner (400)
ansible dev -b -m shell -a "chmod 400 sample.txt"

# 4. Verify the new permissions
ansible dev -b -m shell -a "ls -l"

# 5. Remove the file
ansible dev -b -m shell -a "rm -f sample.txt"
```

### Directory Operations

```bash
# 1. Create a directory named 'demo'
ansible dev -b -m shell -a "mkdir demo"

# 2. List contents to verify creation
ansible dev -b -m shell -a "ls"

# 3. Remove the empty directory
ansible dev -b -m shell -a "rmdir demo"

# 4. Create a directory and set its permissions (777) in one command
ansible dev -b -m shell -a "mkdir demo && chmod 777 demo"

# 5. Verify the permissions
ansible dev -b -m shell -a "ls -ld demo"
```

---

## 🔄 File Transfers (Copy & Fetch)

### `copy` module
Copies a file from your local machine (control node) to the remote servers.

```bash
# Copies a local file to the remote servers
# Note: 'src' is the path on your machine, 'dest' is the path on the remote machine.
ansible dev -b -m copy -a "src=/path/on/your/machine/sam.txt dest=/home/ansible/sam.txt"
```

### `fetch` module
Fetches (downloads) a file from the remote servers to your local machine.

```bash
# Fetches the file from the remote server and saves it locally.
# 'flat=yes' removes the directory structure and saves the file directly into 'dest'.
ansible dev -b -m fetch -a "src=/home/ansible/sam.txt dest=/home/ansible/fetched_files/ flat=yes"
```

---

## 👤 User & Group Management

These commands use the `user` and `group` modules, which are the correct, idempotent way to manage users and groups in Ansible.

### User Management

```bash
# 1. Create a new user 'tony' with a securely hashed password
# Note: Requires 'passlib' to be installed on the control node.
ansible dev -b -m user -a 'name=tony password="{{ "MyP@ssw0rd123" | password_hash("sha512") }}"'

# 2. Verify the user was created by checking the /etc/passwd file
ansible dev -b -m shell -a "grep tony /etc/passwd"

# 3. Remove the user 'tony'
ansible dev -b -m user -a "name=tony state=absent"
```

### Group Management

```bash
# 1. Create a new group called 'devops'
ansible dev -b -m group -a "name=devops state=present"

# 2. Verify the group was created
ansible dev -b -m shell -a "grep devops /etc/group"

# 3. Remove the group 'devops'
ansible dev -b -m group -a "name=devops state=absent"
```