# ovirt_ansible_backup
A simple method to export running oVirt VMs as OVA using ansible.

See https://blog.silverorange.com/backing-up-ovirt-vms-with-ansible-4c2fca8b3b43for more information.

In order for this to work you must have storage for the VM backups attached to one of your oVirt hosts (and specify that host in the playbook vars). The storage can be a local partition/disk or network mounted such as NFS. In the example we use an NFS mount at `/backup` on `host0`. Due to the fact the `wait_for` module uses filenames to allow exporting of one VM at a time the storage should also be accessible from whever you are running the playbook from (in our case we run from the oVirt hosted engine VM with `/backup` mounted on it). It's easy to get started with ansible on the oVirt hosted engine VM as it already has ansible and ovirt python packages installed.

The CA certificate should be available in the same location specified in playbooks on the oVirt hosted engine VM. It should also be possible to download the CA through via the oVirt admin e.x. https://example.com/ovirt-engine/services/pki-resource?resource=ca-certificate&format=X509-PEM-CA

Fill in the rest of the vars as needed and pay special attention to the timeout values, especially if you intend to export large VMs.

Run the playbook using `ansible-playbook backup_ovirt_vms.yml` -- add a crontab entry to automate the process.

## Relevant ansible modules used:

* https://docs.ansible.com/ansible/latest/modules/ovirt_vm_module.html
* https://docs.ansible.com/ansible/latest/modules/ovirt_auth_module.html
* https://docs.ansible.com/ansible/latest/modules/wait_for_module.html
* https://docs.ansible.com/ansible/latest/modules/shell_module.html
