# PREREQUISITES
- Ansible Engine v2.8.0 or higher.
- BIG-IP Setup and Configured

## Overview of Use Case

This use case will configure the BIG-IP To modify an existing ASM Policy to Block IP's and URL's.  
  
**Note: This Use case can be used in an either/or or combined scenario, meaning you can Block URLs or IPs or Both.  This Playbook will also detect if Blocked URL or IP already exists and only add what is new.**

## Per workshop Setup

Now you can start to provision a Lab Environment in AWS.

1. Confiure f5_vars.yml to reflect your environment under provisioning.
  ```yaml
        ASM_Policy_Name: "Demo"
        ASM_Policy_File: "/tmp/XML-Policy.xml"
        F5_IPAddress: 10.192.1.219
        F5_Admin_Port: '443'
        F5_Username: admin
        F5_Password: VMware123!
        Blocked_URLs:
          - /blocked.html
          - /hacked.html
          - /robot.txt
        Blocked_IPs:
          - 10.192.1.199
          - 10.105.192.199
          - 172.16.192.199
          - 192.168.30.199
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

        ansible-playbook F5-ASM-URL-IP-Blocking.yaml -e @f5_vars.yml
        
