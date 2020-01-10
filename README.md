Original OpenShift Ansible repository and Centos 7.6.1810 referenced. And used version 3.11. So before you start the use, please be sure you make 'git checkout release-3.11'<br/>
https://github.com/openshift/openshift-ansible

## PREREQUIREMENTS:

## Preparing the Hosts
All hosts file must be like below (hostnames need to be same 'cat /etc/hostname' output): <br/>
```
192.168.1.101 okd-loadbalancer ahmetmyuksel.local

192.168.1.102 okd-master-1
192.168.1.103 okd-master-2
192.168.1.104 okd-master-3

192.168.1.105 okd-infra-1
192.168.1.106 okd-infra-2
192.168.1.107 okd-infra-3

192.168.1.108 okd-node-1
192.168.1.109 okd-node-2
192.168.1.110 okd-node-3
```

## Network Interfaces
Add below rows to active network interfaces.
```
NM_CONTROLLED="yes"
PEERDNS="yes"
```
<br/>

## Example of Keepalived Configurations (for loadbalancer)
```
vrrp_instance VRRP {
    interface ens192
    virtual_router_id 110
    state MASTER
    priority 200
    advert_int 1
    virtual_ipaddress {
        192.168.1.100 dev ens192
    }
}
```

## Then start the installations:
ansible-playbook -i hosts.ini playbooks/prerequisites.yml  
ansible-playbook -i hosts.ini playbooks/deploy_cluster.yml
