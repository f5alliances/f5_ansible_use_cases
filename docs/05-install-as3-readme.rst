Use Case 05: Install and enable AS3 
===================================

Prerequisites
-------------

This usecase assumes that a F5 BIG-IP instance, webservers and Ansible node are deployed. 
To deploy infrastructure in AWS users can use the `F5 Ansible Provisioner <https://github.com/f5alliances/f5_provisioner>_`


Overview of Use Case
--------------------

This use case will download the latest `AS3 RPM package <https://github.com/F5Networks/f5-appsvcs-extension/releases>_` and install it on the BIG-IP.

Application Services 3 Extension (referred to as AS3 Extension or more often simply AS3) is a flexible, low-overhead mechanism for managing
application-specific configurations on a BIG-IP system.

.. note::
  
   This use case only validates that AS3 has been installed via the playbook. 
   More use cases for AS3 will be added later

Use Case Setup
--------------

1. Login to the Ansible Host 

2. Launching the Ansible Playbook:

   .. code::

      cd ~/f5_ansible_use_cases/05-install-as3
      ansible-playbook F5-Install-AS3-Package.yaml

3. Testing and Validating

   - Login to the BIG-IP
   - Navigate to iApps->Packet Management LX 
   - Veirfy the AS3 RPM package is installed

   |
   .. image:: images/UseCase5-960.gif
   |
