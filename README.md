Here the bios pipeline will be installed on a ubuntu VM together with conda

To run this playbook ansible 2.1 or higher should be installed on the computer that runs this. The remote computer does not require ansible.

### Vagrant

To run this playbook within vagrant the following requirements are needed:
- Anisble installed
- VirtualBox installed
- Vagrant installed

If the machine is not up yet run the follow command withing this directory:
```
vagrant up
```

If this is the first time provision with ansible will start automaticly. To manual start provision when the VM is already up please use:
```
vagrant provision
```


### Remote machine

To run this playbook on a remote machine the following requirements are needed:
- Ansible installed on local machine
- Ubuntu installed on remote machine
- Ssh deamon is enabled on remote machine
- Optional: Account need to be accesable with a ssh key (is not you need to enable an option in ansble that he ask for a password)

In the [invertory.yml] file the nodes where to install this playbook on are listed. Here you can also selected an account name to use on te remote machine.

To execute the playbook run the following command:
```
ansible-playbook -i invertory.yml playbook.yml
```

