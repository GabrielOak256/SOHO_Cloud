# SOHO_Cloud
An internal-only cluster of devices that support a network of containerized workstations.

You may be familiar with Active Directory's Group Policy. I wanted a FOSS equivalent that would advantage the copy-and-paste capability of virtual image templates. This is intended to be deployed in small businesses, operations too small to have IT/Sec staff. A home network is full of individual's devices that must persistently maintain personal files. And an enterprise network has a wide specialized staff with a high budget and their own processes and procedures. 

Imagine all users, when they log into their workstation's SSO panel, are spinning up a container desktop. All persistent application data goes in the NAS - which is strictly governed by LDAP - and when they log off, the container file is wiped out along with any malware that might have infected them. 

The amount of CPU and RAM in a single machine that it would take to support all workstations can be achieved by clustering the small business's existing workstations. 

1.  Back up all data, partition away most of each workstation's disk.
2.  Flash the boot partition with a clean install of whichever form of Linux each machine supports. 
3.  Make each machine into a Kubernetes worker. (I'm not sure if, at this scale, full K8s would be appropriate, or if K3s, K0s, or MicroK8s would be less prone to misconfigurations over time.) I've heard that Podman runs more securely than Docker, but am unfamiliar with both. 
4.  The rest of each disk would be (nfshare) given to a NAS manager running in a container, to assemble them all into a single failure-tolerant volume. 
5.  An OpenLDAP application (I only know of FreeIPA.) would run in another container to keep track of each worker's access. (We should reinforce the access permissions by Veracrypt encrypting protected subdirectories, and only giving keys to approved systems' keychains.)
6.  This cluster should run a couple instances of (preconfigured) OpenWRT/OPNSense for failure tolerance. The hardware firewall/router shouldn't be tossed out because Kubernetes may go down and the potential circular dependency. But a load-balancing solution that connects the modem to the hardware firewall/router as well as the containerized ones running on traditional hardware might be implemented. 
7.  The wireless cards of all cooperating machines can be handed over to make a mesh network. 
8.  A SIEM system would be another appropriate organ of this creature. I've read that the ELK stack is FOSS, but struggled to find information on running and configuring it locally. 

All container images described above would be configured automatically by an IaC solution. 


At this point, the sky's the limit. Instead of group policy, container workstation images can be set up with minimal permissions. The same machines themselves (with their monitors and keyboards) can be used to access this cluster and request a workstation. 



A potential selling point for small businesses to adopt this (besides the security if all is properly configured) is that spare RAM and CPU can be rented out to others or used to mine Bitcoin. 
