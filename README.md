# SOHO_Cloud
A hypothetical plan for a internal-only cluster of devices that support a 
network of containerized workstations.
I hope that over the years this becomes a very practical reference for IT/Sec 
technicians looking to configure these services in their networks. 
(K3s is simpler to maintain than K8s. Podman is compatible with Docker, but 
daemonless. Kubernetes can be made to run whole VMs, not just containers.)

You may be familiar with Active Directory's Group Policy. I wanted a FOSS 
equivalent that would advantage the copy-and-paste capability of virtual image 
templates. This is intended to be deployed in small businesses, operations too 
small to have IT/Sec staff. A home network is full of individual's devices that 
must persistently maintain personal files. And an enterprise network has a wide 
specialized staff with a high budget and their own processes and procedures. 


Imagine all users, when they log into their workstation's SSO panel, are 
given a new copy of a desktop container template. All persistent application 
data goes in the NAS - which is strictly governed by LDAP - and when they log 
off, the container file is wiped out along with any malware that might have 
infected them. 

It's a similar concept to QubesOS. However, QubesOS depends on a baremetal 
install so no inderlying infrastructure can compromise it, and is about 
segregating one user's applications from each other. This idea is about 
advantaging virtualization to give every user an ephemeral workspace on a 
cluster of all company hardware resources. 

The company adopting this scheme can use their existing workstations' monitors
and keyboards to "log in over the network" into containers running on the very 
same machines. 

Instead of configuring Group Policy so that machines ask over the network what 
the user is allowed to do, we can instead simply lobotomize the provided 
workspace images. 

With the increased control of exactly how much of each computer is being 
utilized, maybe some day cloud services will be decentralized to many many 
providers running secure enclaves. 


Instead of a network with many servers, think of a creature with many organs.
The firewall/router is how all the organs know of each other, 
the SIEM sees all the workings from above, 
LDAP to know what belongs and what doesn't, 
a GitLab instance to version control the IaC,
a NAS manager to provide the working storage space in the first place, 
incremental storage of all workstation data,
a vulnerability scanner to keep awareness on the health of the cluster, 
all of the workspaces themselves,
