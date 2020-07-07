# Install kubernetes (Master & Node) on RHEL7.x On-Premise with MetalLB using Ansible Playbooks

Note: These playbooks work only on "On-Premise" RHEL 7.x. VMs.
(Not tested on any other Linux flavor).

You can also watch this youtube tutorial that explains step-by-step process to deploy kubernetes using these playbooks:

https://www.youtube.com/watch?v=IAAI9Fes2L0


##  Prerequisites

1. You must be able to run superuser commands on Linux servers through ansible.
You may test it by issuing these command from where you will be running your ansible playbooks:

```
$ ansible master --become -a "tail -1 /var/log/audit/audit.log"

$ ansible node01 --become -a "tail -1 /var/log/audit/audit.log"
$ ansible node02 --become -a "tail -1 /var/log/audit/audit.log"
.
.
```

2. Please make sure the RHEL is already subscribed (attached).

3. Download these files on your ansible control node:

   $ git clone https://github.com/tech-tok/kubernetes-ansible-rhel

## Install Instructions 

Please make sure you modify below file accordingly:

Step1: Set your IP range for MetalLB in : local_files/my-layer2-config.yaml.

This IP range should be from the same Network as your Master/Nodes IP network.

```
      - 192.168.1.100-192.168.1.120
```


Step2: Install kubernetes on the master server called "master":

```
ansible-playbook --become -i master, install_kube_master.yml
```

Step3: Install kubernets on Nodes (node01, node02, [...]) and join the Master (master) automatically:

```
ansible-playbook --become -i node01, install_kube_node.yml
ansible-playbook --become -i node02, install_kube_node.yml
.
.
```

All Done!
