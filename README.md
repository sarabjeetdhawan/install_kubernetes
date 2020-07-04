# install_kubernetes
Ansible Playbooks to install Kubernetes (Master and Nodes) ON-PREMISE with MetalLB

These playbooks works on On-Premise RHEL 7.x. VMs
(Not tested on any other Linux flavor).


****** Prerequisites ******

Please make sure you modify below files accordingly:

1. Set your IP range for MetalLB in : local_files/my-layer2-config.yaml 

```
      - 192.168.1.100-192.168.1.120
```

2. Set your own RHEL credentials in both of the playbooks:

```
  - name: Copy your redhat credentials in docker config (If Applicable)
    copy:
      dest: "/var/lib/kubelet/.dockercfg"
      content: |
        {
             "https://registry.redhat.io": {
                     "auth": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
                     "email": "XYZ@example.com"

             }
        }
```

3. You must be able to run superuser commands on VMs using ansible.
You may test it by issuing this command:

$ ansible master --become -a "cat /etc/shadow"
$ ansible node01 --become -a "cat /etc/shadow"
$ ansible node02 --become -a "cat /etc/shadow"
and so on..


****** Install Instructions ******

Step1: ansible-playbook --become -i master, install_kube_master.yml
Step2: ansible-playbook --become -i node01, install_kube_node.yml
Step3: ansible-playbook --become -i node02, install_kube_node.yml

and so on..

NOTE: During the execution, the playbook would require you to manually run this command on the Master and Node as root.
      The playbook will pause for 2 minutes for you to complete that manual step:

# yum list installed kubeadm -y

