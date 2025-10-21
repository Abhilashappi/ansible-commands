# Ansible module Command Examples

This repository serves as a practical guide and cheat sheet for using Ansible module commands to manage remote servers.

## 📖 About This Project

The main file, `ansible_cmds.md`, contains a curated list of commands for performing common system administration tasks. These examples are designed to be clear, easy to understand, and ready to use.

The commands cover several key areas of server management:

* **File & Directory Management**: Using the `shell` module for creating, modifying, and removing files and directories.
* **File Transfers**: Leveraging the `copy` and `fetch` modules to move files between your control node and remote hosts.
* **User & Group Management**: Demonstrating the correct, idempotent way to manage users and groups with the `user` and `group` modules.

## 🚀 How to Use

Simply browse the `ansible_cmds.md` file to find the command you need for a specific task. The commands are commented to explain what each one does.

## ✅ Prerequisites

Before running these commands, please ensure your environment is set up correctly:

1.  **Ansible Inventory**: You need an inventory file (e.g., `/etc/ansible/hosts`) with a defined group of hosts. The examples use a group named `dev`.
2.  **Passlib Library**: For password hashing with the `user` module, the `passlib` library must be installed on your control node.
    ```bash
    sudo apt install python3-passlib
    ```