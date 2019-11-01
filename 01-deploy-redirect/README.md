# PREREQUISITES
- Instance of the [F5 Ansible AWS Provisioner](https://github.com/f5alliances/f5_provisioner) deployed

## Overview of Use Case
This scenario will configure the BIG-IP To create a Redirect to Port 80 from a pre-existing VIP.  

When a BIG-IP has multiple Virtual IPs (VIPs) configured, it can be tedious to implement an SSL (Port 443) redirect from standard HTTP traffic.  This automation playbook will create an SSL VIP then create the assosicative Port 80 SSL redirect for that VIP.

This script can be modified to work on other VIPs by editing the F5_VIP_Name section inside of the f5_vars.yaml
  
**Note: this will loop through the entire VIP list so this could take a long time depending on the amount of VIPs within your BIG-IP**

## Use Case Setup

1. Login to the Ansible Host provided by the F5 Ansible AWS Provisioner 
  ```
   - Use the Workbench information that is stored in a local directory named after the workshop (e.g. TESTWORKSHOP1/instructor_inventory.txt).  Example:
   ```handlebars
   [all:vars]
   ansible_port=22

   [student1]
   student1-ansible ansible_host=34.219.251.xxx ansible_user=centos 
   student1-f5 ansible_host=52.39.228.xxx ansible_user=admin
   student1-host1 ansible_host=52.43.153.xxx ansible_user=centos
   student1-host2 ansible_host=34.215.176.xxx ansible_user=centos
   ```

2. Launching the Ansible Playbook:
```
   ansible-playbook F5-LTM-HTTP-Redirect.yml -e @f5_vars.yml
```
![Use-Case 1](../images/UseCase1-960.gif)

3. Testing and Validing 
```
- Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansbile_host=PUBLIC-IP) using the ansbile_host Public IP on port 8443 (e.g. https://PUBLIC-IP:8443) to view the BIG-IP Admin page 
  
- To view the deployed use case access port 80/443 of the same Public IP Address (e.g. http://PUBLIC-IP) 
``` 
**NOTE: The browser certificate used is the default certificate built with the BIG-IP and will be UNTRUSTED by default.**
