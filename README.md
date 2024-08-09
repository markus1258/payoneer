# payoneer

### The CI
- Will trigger upon push to branch main
- Builds the image for the application located in /payoneer directory

### The CD
- Will trigger upon successful completion of the CI flow
- Imports the SSH key to local runner in order to authenticate to our VM
- Installs python on the local runner in order to install and run ansible
- Runs the ansible playbook using the inventory.ini file to configure our VM
- Runs the Docker image created by the CI flow

### Diagram
https://t.ly/JItmX

### inventory.ini
- includes our vm (ungrouped) with the following arguments:
  - ansible_user to specify centos as the user to connect the VM
  - ansible_ssh_private_key_file to specify the private key we imported to the local runner as part of the CD flow
  - ansible_ssh_extra_args to prevent known_hosts check from the local runner
