# PREREQUISITES
- Instance of the [F5 Ansible AWS Provisioner](https://github.com/f5alliances/f5_provisioner) deployed

## Overview of Use Case
This use case will configure the BIG-IP to provision BIG-IP ASM, create a Virtual IP (VIP) including a Pool and nodes, an ASM Policy for the use case, then modify the created ASM Policy to Block IP's and URL's.  

As a security consious vendor F5 wants to ensure that customers can find automated ways to block bad contenders either by IP or by specific URLs that are being attacked.  This playbook was designed to allow customers to integrate with other security vendors or even ticketing based solutions like Service NOW to create a start to finish automated solution based on when attacks can occur. 

**Note: This Use case can be used in an either/or or combined scenario, meaning you can Block URLs or IPs or Both.  This Playbook will also detect if Blocked URL or IP already exists and only add what is new.**

This script can be modified to work on other URLs or IP's by editing the Blocked_URLs and/or Blocked_IPs section inside of the f5_vars.yaml
  
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
   ansible-playbook F5-ASM-URL-IP-Blocking.yaml -e @f5_vars.yml
```
![Use-Case 3](../images/UseCase3-960.gif)
 
3. Testing and Validating 
```
- Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansible_host=PUBLIC-IP) using the ansible_host Public IP on port 8443 (e.g. https://PUBLIC-IP:8443) to view the BIG-IP Admin page 
  
- To view the deployed use case access port 8082 of the same Public IP Address (e.g. https://PUBLIC-IP:8082) 
``` 
