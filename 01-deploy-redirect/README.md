# PREREQUISITES
- Ansible Engine v2.8.0 or higher.
- BIG-IP Setup and Configured

## Overview of Use Case

This use case will configure the BIG-IP To create a Redirect to Port 80 from a pre-existing VIP.  
  
**Note: this will loop through the entire VIP list so this could take a long time depending on the amount of VIPs within your BIG-IP**

## Use Case Setup

1. Confiure f5_vars.yml to reflect your environment under provisioning.
  ```yaml
        # Modify based on deployment
        F5_IPAddress: 10.192.1.219
        F5_Admin_Port: '443'
        F5_Username: admin
        F5_Password: VMware123!
        F5_VIP_App_Name: Test2-VIP
  ```
   - if using F5_Provisioner use the Workbench information that is stored in a local directory named after the workshop (e.g.    TESTWORKSHOP1/instructor_inventory.txt).  Example:
   ```handlebars
   [all:vars]
   ansible_port=22

   [student1]
   student1-ansible ansible_host=34.219.251.xxx ansible_user=centos 
   student1-f5 ansible_host=52.39.228.xxx ansible_user=admin
   student1-host1 ansible_host=52.43.153.xxx ansible_user=centos
   student1-host2 ansible_host=34.215.176.xxx ansible_user=centos
   ```

2. Using Ansible Playbook:
   ```
   ansible-playbook F5-LTM-HTTP-Redirect.yml -e @f5_vars.yml
   ```        
