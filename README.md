🔐 Ansible Root Password Reset with Vault

This repository contains an Ansible playbook designed to securely reset the root user password on remote Linux hosts using Ansible Vault for password encryption.

📁 Repository Structure

.
├── password_reset_using_vault.yml   # Main playbook to reset root password
├── vault.yml                        # Encrypted file storing the root password
├── servers                          # Inventory file listing target hosts
└── README.md                        # Project documentation (this file)
