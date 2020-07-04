# install_kubernetes
Ansible Playbooks to install Kubernetes (Master and Nodes) ON-PREMISE with MetalLB

These playbooks work on "On-Premise" RHEL 7.x. VMs.
(Not tested on any other Linux flavor).

****** Prerequisites ******

Please make sure you modify below files accordingly:

1. Set your IP range for MetalLB in : local_files/my-layer2-config.yaml 

```
      - 192.168.1.100-192.168.1.120
```

2. You must be able to run superuser commands on Linux servers through ansible.
You may test it by issuing these command from where you will be running your ansible playbooks:


```
$ ansible master --become -a "cat /etc/shadow"
$ ansible node01 --become -a "cat /etc/shadow"
$ ansible node02 --become -a "cat /etc/shadow"
```
and so on..


****** Install Instructions ******

Step1: Install kubernetes on the master server called "master":

```
ansible-playbook --become -i master, install_kube_master.yml
```

Step2: Install kubernets on Nodes (node01, node02) and join the Master (master):

```
ansible-playbook --become -i node01, install_kube_node.yml
ansible-playbook --become -i node02, install_kube_node.yml
```

and so on..

NOTE: During the execution, the playbook would pause for 2 minutes and require you to manually run this command on the Master and Node(s) as root.

# yum list installed kubeadm -y

