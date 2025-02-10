# ansible-deploy-django
Deploy Django app using Ansible playbook

# README: Running the Ansible Playbook

## Prerequisites

Before running the playbook, ensure you have the following installed:

- Ansible (Install using `sudo apt update && sudo apt install -y ansible`)
- SSH access to the target servers
- A valid `inventory.ini` file with the correct server details
- A properly configured SSH key for authentication

## Setup Inventory File (`inventory.ini`)

Create an `inventory.ini` file with the target servers. Example format:

```ini
[webservers]
HOST_IP_ADDRESS ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/key.pem



Modify this file to match your server details.

## Running the Ansible Playbook

1. Ensure you are in the correct directory where the playbook and inventory file are located.
2. Run the following command to execute the playbook:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

### Running a Specific Tag

To run a specific task using tags, use:

```bash
ansible-playbook -i inventory.ini playbook.yml --tags "tag_name"
```

### Running in Check Mode (Dry Run)

To preview changes without applying them:

```bash
ansible-playbook -i inventory.ini playbook.yml --check
```

## Debugging and Logs

To increase verbosity for debugging, add `-vvv`:

```bash
ansible-playbook -i inventory.ini playbook.yml -vvv
```

## Updating Permissions

If you face permission issues with your SSH key, run:

```bash
chmod 400 /path/to/key.pem
```

## Notes

- Ensure the target server's security group allows SSH access.
- If the playbook modifies system services, ensure you have appropriate privileges.
- Modify the `inventory.ini` file as needed for different environments.

## Troubleshooting

1. **Permission Denied (Public Key Error)**:

   - Verify the correct SSH key is being used.
   - Ensure the key has the right permissions (`chmod 400 key.pem`).
   - Ensure the key is added to `~/.ssh/authorized_keys` on the remote server.

2. **SSH Connection Issues**:

   - Use `ansible -i inventory.ini all -m ping` to test connectivity.
   - Check security group and firewall settings to allow SSH access.

3. **YAML Syntax Errors**:

   - Validate the playbook using:
     ```bash
     ansible-playbook playbook.yml --syntax-check
     ```

## References

- [Ansible Documentation](https://docs.ansible.com/)
- [AWS EC2 SSH Troubleshooting](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html)


