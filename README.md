# Ansible lab automation as a part of Network automation course.

Table of contents

1. [ Enviroment Overview.](#env)
2. [ Network Topology. ](#net)
3. [ Ansible configuration. ](#ans)
4. [ Playbooks. ](#play)


<a name="env"></a>
## 1. Enviroment Overview

This lab is built in EVE-NG, is a network virtualisation platform which an interface to building virtual network topologies of many vendors of networking equipment

<a name="net"></a>
## 2. Network Topology

In this lab is the management interfaces are pre-configures with the following Routers:

R2 192.168.170.182

R3 192.168.170.183

R4 192.168.170.184

R5 192.168.170.185

R6 192.168.170.186

R7 192.168.170.187

All Routers have a interface in Management-NAT(vmnet1), which is Routers through the management vmnet1 to the outside, towards the Ansible host.


<img src="images/netlab.jpg">


<a name="ans"></a>
## 3. Ansible Configuration



<a name="play"></a>
## 4. Playbooks



Environment description Topology description Ansible configuration Implemented playbooks

Environment description

The lab is built in a VMware 6.5 ESXi host. It consists of two virtual servers:

Eve-NG: This is a network virtualisation platform which an interface to building virtual network topologies of many vendors of networking equipment. Eve-NG

Linux server: This server hosts the ansible lab environment. It is running Ubuntu 18.04 LTS, and Ansible 2.7 is installed.

Both servers have two NICs, which are both are connected through a separate standard vswitch. The first NIC has a connection to the corporate network, and provides connectivity to the internet using NAT provided by the corporate firewall infrastructure. The second NIC is connected to a vswitch which only connects the Linux server with the Eve-NG server to allow access to the switches running on Eve-NG.

Local vswitch topology:

Topology description


<img src="images/netlab.jpg">




sometext

On Eve-NG there runs a virtual network environment with the following switches:

hostname IP Description s11-iol 10.100.1.11 Cisco IOL virtual switch s12-iol 10.100.1.12 Cisco IOL virtual switch s13-iol 10.100.1.13 Cisco IOL virtual switch s14-iol 10.100.1.14 Cisco IOL virtual switch s15-iol 10.100.1.15 Cisco IOL virtual switch mgmt-iol 10.100.1.100 Cisco IOL virtual switch used for aggregation and uplink to ansible host  10.100.1.20 Ansible host All switches have a interface in a switch management vlan, which is switched through the management switch (mgmt-iol) to the outside, towards the Ansible host.

Ansible configuration

At the start of the course, the Ansible configuration is still basic. Here is an overview of the files currently in use:

File Description ansible.cfg Standard ansible configuration file, with tweaks for vault and inventory location inventory Basic static inventory file listing all switches in the lab environment group_vars/lab/vars placeholder for global variables related to the lab group group_vars/lab/vault placeholder for vault variables related to the lab group (currently contains ssh password for Cisco switches) Example of raw adhoc command:



:~/ansible_lab$ ansible -m raw -a "show run | i hostname" lab s12-iol | CHANGED | rc=0 >> hostname s12-iol Shared connection to s12-iol closed.

s14-iol | CHANGED | rc=0 >> hostname s14-iol Shared connection to s14-iol closed.

s11-iol | CHANGED | rc=0 >> hostname s11-iol Shared connection to s11-iol closed.

s13-iol | CHANGED | rc=0 >> hostname s13-iol Shared connection to s13-iol closed.

s15-iol | CHANGED | rc=0 >> hostname s15-iol Shared connection to s15-iol closed. Implemented playbooks

backup_config.yml: Playbook which reads config from all hosts and stores it in the device_config directory. Changes are also commited to the repository

napalm_get_facts.yml: Basic playbook to get napalm facts from devices. A filter can be specified when running the playbook.

cisco_lldp_topo.yml: (2nd course assignment) Playbook wheach reads config from all hosts and tries to build an LLDP topology graph using graphviz

cisco_provisioning.yml: (3rd/4th course assignment) Playbook which generates and installs basic cisco device config.

cisco_vlan_service.yml: (3rd/4th course assignment) Playbook which generates and installs cisco config for provisioning a layer 2 vlan service per port.

cisco_validate.yml: (3rd/4th course assignment) Playbook which does a config check to see if the live config is as intended.

More to be added as the course progresses
