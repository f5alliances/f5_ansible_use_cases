# PREREQUISITES
- Instance of the [F5 Ansible AWS Provisioner](https://github.com/f5alliances/f5_provisioner) deployed

## Overview of Use Case
This use case will configure the BIG-IP To Enable or Disable LTM Pool Members.  

There are times where servers must be taken offline to provide upgrades, troubleshooting, or even replacement.  This script allows the ability to enable or disable members within a pool.  This playbook allows the ability to enable/disable all pool members (all) or by host name (e.g. host1:80) 

**Note: There is an addtional extra_var within the playbook call to trigger the enable or disable**
  
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
 # To Enable Pool Members
 ansible-playbook F5-LTM-Member-Enable-Disable.yaml -e @f5_vars.yml -e "pool_action=enable"
 
 # To Disable Pool Members
 ansible-playbook F5-LTM-Member-Enable-Disable.yaml -e @f5_vars.yml -e "pool_action=disable"
```
![Use-Case 4](../images/UseCase4-960.gif)
 
3. Testing and Validating 
```
- Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansible_host=PUBLIC-IP) using the ansible_host Public IP on port 8443 (e.g. https://PUBLIC-IP:8443) to view the BIG-IP Admin page 
  
- To view the deployed use case access port 8083 of the same Public IP Address (e.g. https://PUBLIC-IP:8083) 
``` 
