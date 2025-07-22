🔐 Ansible Root Password Reset with Vault

This repository contains an Ansible playbook designed to securely reset the root user password on remote Linux hosts using Ansible Vault for password encryption.

📁 Repository Structure

.
├── password_reset_using_vault.yml   # Main playbook to reset root password
├── vault.yml                        # Encrypted file storing the root password
├── servers                          # Inventory file listing target hosts
└── README.md                        # Project documentation (this file)

📋 Prerequisites

Before running the playbook, ensure you have the following:

Ansible installed (ansible --version)
SSH access to all listed hosts (using the ansible_user and ansible_password)
Encrypted vault.yml file containing the root password
A vault password file or prompt to decrypt vault.yml
🔐 Step 1: Encrypt the Vault File

To store the root password securely, create and encrypt the vault.yml file:

ansible-vault create vault.yml
When prompted, add the following content:

vault_root_password: '<hashed_password>'
Replace <hashed_password> with a hashed password. You can generate a hashed password using openssl or python.

Example using Python:

python3 -c 'import crypt; print(crypt.crypt("9422", "$6$saltsalt"))'
Copy the output (something like $6$saltsalt$...) into your vault.yml file.

🧾 Example Encrypted vault.yml
vault_root_password: '$6$saltsalt$W9NvZb1X/...'
Save and exit. This file will now be encrypted.

🧪 Step 2: Verify Your Inventory

Ensure your servers inventory file contains the correct IPs and credentials:

[all]
54.235.28.136 ansible_user=komal ansible_password=5912
34.227.24.18 ansible_user=komal ansible_password=5912
⚠️ Note: Avoid committing real passwords or IPs to a public repo. Use Ansible Vault or .gitignore for security.
🚀 Step 3: Run the Playbook

Execute the playbook with the following command:

ansible-playbook -i servers password_reset_using_vault.yml --ask-vault-pass
Or use a vault password file:

ansible-playbook -i servers password_reset_using_vault.yml --vault-password-file .vault_pass.txt
📌 Notes

This playbook resets the root password on all hosts listed in the inventory.
You must use a hashed password, not plaintext.
Ansible Vault ensures your password is encrypted and secure.
🔐 Security Tips

Always use encrypted vault files to store sensitive information.
Avoid pushing sensitive data to public repositories.
Regularly rotate passwords and vault keys.
🛠️ Troubleshooting

Authentication fails? Check your ansible_user and ansible_password in the inventory.
Vault decryption fails? Ensure you're using the correct vault password or file.
No password change? Ensure your hashed password is valid and has proper format ($6$ for SHA-512).
📄 License

This project is licensed under the MIT License.



