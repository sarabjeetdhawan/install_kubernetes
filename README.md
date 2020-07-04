# Install kubernetes (Master & Node) on RHEL7.x On-Premise with MetalLB using Ansible Playbooks

Note: These playbooks work only on "On-Premise" RHEL 7.x. VMs.
(Not tested on any other Linux flavor).

##  Prerequisites

Please make sure you modify below file accordingly:

1. Set your IP range for MetalLB in : local_files/my-layer2-config.yaml 
This IP range should be from the same Network as your Master/Nodes IP network.

```
      - 192.168.1.100-192.168.1.120
```

2. You must be able to run superuser commands on Linux servers through ansible.
You may test it by issuing these command from where you will be running your ansible playbooks:

```
$ ansible master --become -a "/usr/sbin/lvm lvs"

$ ansible node01 --become -a "/usr/sbin/lvm lvs"
$ ansible node02 --become -a "/usr/sbin/lvm lvs"
```
and so on...

3. Please make sure the RHEL is already subscribed (attached).


## Install Instructions 

Step1: Install kubernetes on the master server called "master":

```
ansible-playbook --become -i master, install_kube_master.yml
```

Step2: Install kubernets on Nodes (node01, node02, [...]) and join the Master (master) automatically:

```
ansible-playbook --become -i node01, install_kube_node.yml
ansible-playbook --become -i node02, install_kube_node.yml
```

and so on..
