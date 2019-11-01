## PREREQUISITES
Instance of the [F5 Ansible AWS Provisioner](https://github.com/f5alliances/f5_provisioner) deployed

## Overview of Use Case
This scenairo will configure the BIG-IP To import certificates (cert/key), create (if doesnt already exist) a Virtual IP (VIP), a Pool and ClientSSL Profile and assign it to the created VIP (Use-Case-2).

Being able to create and swap SSL Profiles on a BIG-IP to singular or multiple VIPs is extremly useful, especially in today's world where SSL keys get leaked or hacked or expire.  This automated method allows a seamless process to create and change certificates based on need/demand.

This script can be modified to work on other VIPs by editing the F5_VIP_Name section inside of the f5_vars.yaml
  
## Use Case Setup

1. Login to the Ansible Host provided by the F5 Ansible AWS Provisioner 
 
   Use the Workbench information that is stored in a local directory named after the workshop (e.g. TESTWORKSHOP1/instructor_inventory.txt).  Example:
   
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
   cd ~/f5_ansible_use_cases
   ansible-playbook F5-LTM-Cert-Management-Replacement.yaml -e @f5_vars.yml
   ```

   <kbd>
    <img src="../images/UseCase2-960.gif">
   </kbd>   

   <br/>
  
3. Testing and Validating 
   - Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansible_host=PUBLIC-IP) using the ansible_host Public IP on port 8443 (e.g. https://PUBLIC-IP:8443) to view the BIG-IP Admin page 
   - To view the deployed use case access port 8081 of the same Public IP Address (e.g. https://PUBLIC-IP:8081) 

**NOTE: The browser certificate used in this scenario is a "Self Signed" UNTRUSTED Certificate.**

