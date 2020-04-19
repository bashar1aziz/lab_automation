# Ansible lab automation.

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


| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

R2 192.168.170.182

R3 192.168.170.183

R4 192.168.170.184

R5 192.168.170.185

R6 192.168.170.186

R7 192.168.170.187

All Routers have a interface in Management-NAT(vmnet1), which is Routers through the management vmnet1 to the outside, towards the Ansible host.


<img src="images/lab_auto.png">


<a name="ans"></a>
## 3. Ansible Configuration



<a name="play"></a>
## 4. Playbooks



