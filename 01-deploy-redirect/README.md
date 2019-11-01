# PREREQUISITES
- This usecase assumes that a F5 BIG-IP instance, webservers and Ansible node are deployed. To deploy infrastructure in AWS users can use the [F5 Ansible Provisioner](https://github.com/f5alliances/f5_provisioner)

## Overview of Use Case
Challenge: When a BIG-IP has multiple Virtual IPs (VIPs) configured, it can be tedious to implement an SSL redirect from standard HTTP traffic for each Virtual IP. 

F5-LTM-HTTP-Redirect.yml playbook will create an SSL VIP then create the associative Port 80 SSL redirect for that VIP.

In this example, the playbook looks for F5_VIP_Name: 'Use-Case-1-VIP' as specified in the f5_vars.yaml variable file. Users can modify this variable file to create redirect service for any other VIP. 
  
**Note: this will loop through the entire VIP list so this could take time depending on the number of VIPs within your BIG-IP**

## Use Case Setup

1. Login to the Ansible Host. 
Code below is based on infrastructure components provisioned by the [F5 Provisioner](https://github.com/f5alliances/f5_provisioner). TESTWORKSHOP1/instructor_inventory.txt file will contain the Workbench information. Example:

```handlebars
   [all:vars]
   ansible_port=22

   [student1]
   student1-ansible ansible_host=10.10.10.11 ansible_user=centos #ansible host
   student1-f5 ansible_host=10.10.10.21 ansible_user=admin #F5 BIG-IP
   student1-host1 ansible_host=10.10.10.31 ansible_user=centos #Webserver1
   student1-host2 ansible_host=10.10.10.32 ansible_user=centos #webserver2
```

2. Running the Ansible Playbook 'F5-LTM-HTTP-Redirect.yml' with the variable file 'f5_vars.yml' :
```
   cd ~/f5_ansible_use_cases
   ansible-playbook F5-LTM-HTTP-Redirect.yml -e @f5_vars.yml
```
![Use-Case 1](../images/UseCase1-960.gif)
 
3. Testing and Validating 
  - Using the workbench information Login to the BIG-IP (e.g. student1-f5 ansible_host=10.10.10.21:8443) and ensure there is 2 VIPs with same IP - one with port 443 and one with port 80
  - You should be able be redirected to 443 when you try to access VIP:80. The same webpage will also be accessible via VIP:443
 
**NOTE: While accessing the Virtual IP, your browser is presented with a certificate (clientssl cert) that is built with the BIG-IP. You will therefore see an 'unsafe' message. Click proceed to website.**
