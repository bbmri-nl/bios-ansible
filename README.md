Instructions on auto-deploying BBMRI BIOS pipeline using ansible, conda and biopet framework.
==============

Prerequisite
=====
* On the managing computer, Ansible 2.0 or higher is required to run the playbook. 
* On the managed computer/VM, Ubuntu (tested on 14.04) with SSH and a user account (sudo is not necessary) is required. Gcc should be installed already.

Test with Vagrant
=====

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

Deploy pipeline and all its dependency on a remote server/VM
=====

In the [invertory.yml] file the nodes where to install this playbook on are listed. Here you can also selected an account name to use on the remote machine.

To execute the playbook run the following command on the managing computer:
```
ansible-playbook -i invertory.yml playbook.yml
```

Run pipeline with tested dataset
=====

Define samples in samples.yml:
``` yaml
samples:
  sample1:
    libraries:
      lib1:
        R1: <Path to R1 fq>
        R2: <Path to R2 fq>
  sample2:
    libraries:
      lib1:
        R1: <Path to R1 fq>
        R2: <Path to R2 fq>

```

Running a dry run of the pipeline:
```
bios-pipeline -config <samples.yml> -cv output_dir=<output_dir>
```

Running the pipeline with:
```
bios-pipeline -config <samples.yml> -cv output_dir=<output_dir> -run
```

Running multiple jobs in parallel:
```
bios-pipeline -config <samples.yml> -cv output_dir=<output_dir> -maxConcurrentRun 10  -jobRunner ParallelShell -run
```
