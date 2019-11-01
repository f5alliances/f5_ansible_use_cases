## PREREQUISITES
Instance of the [F5 Ansible AWS Provisioner](https://github.com/f5alliances/f5_provisioner) deployed

## Overview of Use Case
This use case will download the latest AS3 Module and install it on the BIG-IP.  

Application Services 3 Extension (referred to as AS3 Extension or more often simply AS3) is a flexible, low-overhead mechanism for managing application-specific configurations on a BIG-IP system. 

**Note: This use case only validates that AS3 has been installed via the playbook.  More use cases for AS3 will be added later**
  
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
   ansible-playbook F5-Install-AS3-Package.yaml
   ```
   
   <kbd>
    <img src="../images/UseCase5-960.gif">
   </kbd>   

   <br/> 
   
3. Testing and Validating 
   - Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansible_host=PUBLIC-IP) using the ansible_host Public IP on port 8443 (e.g. https://PUBLIC-IP:8443) to view the BIG-IP Admin page 
   
