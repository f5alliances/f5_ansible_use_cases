## Extra-Variables in Ansible Tower  

```
F5_IPAddress: 10.192.1.219
F5_Admin_Port: '443'
F5_Username: admin
F5_Password: VMware123!
F5_VIP_Name: Test-VIP
F5_New_Pool_LB_Method: least-connections-member

F5_New_Pool_Monitors: "http"
#How to add multiple monitors vs single monitor
#F5_New_Pool_Monitors: "http,gateway_icmp"

#- Only works if F5_Pool_Name Exists and F5_New_Pool_Members doesnt exist (Commented out or missing)
#F5_Pool_Name: http-pool

#F5_New_Pool_Members is a multi-variable array to allow for IP/Port Combos
F5_New_Pool_Members: 
- {"IP": "192.168.30.50", "Port": "443"}
- {"IP": "192.168.30.51", "Port": "80"}
- {"IP": "192.168.30.52", "Port": "22443"}
```


# PREREQUISITES
- Ansible Engine v2.8.0 or higher.
- BIG-IP Setup and Configured

## Overview of Use Case

This use case will configure the BIG-IP To create or use existing pool to assign to a pre-existing VIP.  
  
**Note: When F5_New Pool Members is defined then the assumption is new poool is created, if not defined then uses existing pool to assign to VIP**

## Use Case Setup

1. Confiure f5_vars.yml to reflect your environment under provisioning.
  ```yaml
        F5_IPAddress: 10.192.1.219
        F5_Admin_Port: '443'
        F5_Username: admin
        F5_Password: VMware123!
        F5_VIP_Name: Test-VIP
        F5_New_Pool_LB_Method: least-connections-member

        F5_New_Pool_Monitors: "http"
        #How to add multiple monitors vs single monitor
        #F5_New_Pool_Monitors: "http,gateway_icmp"

        #- Only works if F5_Pool_Name Exists and F5_New_Pool_Members doesnt exist (Commented out or missing)
        #F5_Pool_Name: http-pool

        #F5_New_Pool_Members is a multi-variable array to allow for IP/Port Combos
        F5_New_Pool_Members: 
        - {"IP": "192.168.30.50", "Port": "443"}
        - {"IP": "192.168.30.51", "Port": "80"}
        - {"IP": "192.168.30.52", "Port": "22443"}
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

        ansible-playbook F5-LTM-New-Pool.yaml -e @f5_vars.yml
        
