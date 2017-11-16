Instructions on auto-deploying BBMRI BIOS pipeline using ansible, conda and biopet framework.
==============

BBMRI BIOS pipeline
=====
The RNAseq pipeline that can be deployed using this Ansible script is the exact replication of the RNAseq pipeline used by this Nature Genetics paper (www.nature.com/ng/journal/v49/n1/full/ng.3737.html). For more background information, please read its method section.

Prerequisite
=====
* Please read the general introduction of Ansible first: http://docs.ansible.com/ansible/latest/intro_getting_started.html#
* A basic understanding of (Bio-)Conda is good to have, but not really required if you just want to deploy this BBMRI BIOS pipeline.
* On the managing computer, Ansible 2.0 or higher is required to run the playbook. 
* On the managed computer/VM, Ubuntu (tested on 14.04) with SSH and a user account (sudo is not necessary) is required.
 - Gcc and libxrender should be installed already.

Test with Vagrant
=====

To run this playbook within vagrant the following requirements are needed:
- Anisble installed
- VirtualBox installed
- Vagrant installed (version 1.5.x and above)

If the machine is not up yet run the follow command withing this directory:
```
vagrant up
```

If this is the first time provision, ansible will start automatically. To manually start provision when the VM is already up please use:
```
vagrant provision
```

Deploy pipeline and all its dependency on a remote server/VM
=====

In the [invertory.yml] file the nodes where to install this pipeline are listed. Here you can also define a user account to use on the remote machine.

To execute the playbook run the following command on the managing computer:
```
ansible-playbook -i inventory.yml playbook.yml
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
