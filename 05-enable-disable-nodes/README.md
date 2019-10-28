# PREREQUISITES
- Ansible Engine v2.8.0 or higher.
- BIG-IP Setup and Configured

## Overview of Use Case

This use case will configure the BIG-IP To Enable or Disable LTM Nodes.  
  
**Note: This script will only allow to Disable OR Enable nodes it cannot do both at the same time**

## Use Case Setup

1. Confiure f5_vars.yml to reflect your environment under provisioning.
  ```yaml
        # Modify based on deployment
        F5_IPAddress: 10.192.1.219
        F5_Admin_Port: '443'
        F5_Username: admin
        F5_Password: VMware123!
        #F5_Node_State - can be Enabled or Disabled (case not sensitve)
        F5_Node_State: Disabled
        #F5_Nodes - Must be exact names of Nodes within LTM --> Nodes
        F5_Nodes:
        - 192.168.30.50
        - 192.168.30.51
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

2. Run the playbook 

  - Using Ansible Tower copy the variables out of the f5_vars.yml file and place into the Extra Variables field in the Template.
![f5 diagram](images/Ansible_Tower_Vars.png)

  - (Alternative Option) - Using Ansible Playbook:

        ansible-playbook F5-LTM-HTTP-Redirect.yml -e @f5_vars.yml
        
