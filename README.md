**Quick Guide: Secure Configuration for Debian/Ubuntu**
=========

```
1) File Modifications

  - Update inventory: Replace all parameters with placeholder values denoted by $.

  - Configure ./keys/ssh_keys.yml: This file will contain encrypted SSH keys in the following format:

private_key: |
  -----BEGIN $algorithm PRIVATE KEY-----
  .....................................
  -----END $algorithm PRIVATE KEY-------
public_key: |
 ssh-$algorithm AAAAB3... (public key)

    Steps:
     - Generate an SSH key pair:
         ssh-keygen -t $algorithm
     - Create a file named ssh_keys.yml, add your generated private and public keys, and encrypt it:
         ansible-vault encrypt ssh_keys.yml

  - Edit ./roles/sshd_configure/vars/main.yml: Adjust the variables for user, group, and ssh_key_filename.

2) Run the Playbook

  - Start the playbook with the following command:
      ansible-playbook secure_vm_configure.yml --ask-vault-password

3) Enter the Vault Password

  - When prompted, provide the password to decrypt ssh_keys.yml.
