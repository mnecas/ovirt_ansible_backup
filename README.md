# ovirt_ansible_backup
A simple way to export running oVirt VMs as OVA using ansible.

See <BLOG_POST_URL> for more information.

Note: In order for this to work you must have storage for the VM backups attached to one of your oVirt hosts (and specify that host in the playbook vars). The storage can be a local partition/disk or network mounted such as NFS. In the example we use an NFS mount at /backup on host0. Due to the fact the wait_for module uses filenames to allow exporting of one VM at a time the storage should also be accessible from whever you are running the playbook from (in our case we run from the oVirt hosted engine VM with /backup mounted on it).

Fill in the rest of the vars as needed and pay special attention to the timeout values, especially if you intend to export large VMs.

Links to some of the ansible modules used in this project:

https://docs.ansible.com/ansible/latest/modules/ovirt_vm_module.html#ovirt-vm-module

https://docs.ansible.com/ansible/latest/modules/ovirt_auth_module.html#ovirt-auth-module

https://docs.ansible.com/ansible/latest/modules/wait_for_module.html

https://docs.ansible.com/ansible/latest/modules/command_module.html#command-module

