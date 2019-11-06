F5 AUTOMATION ANSIBLE USE CASES
===============================

Overview
--------

The Use Cases for the F5 Automation Provisioner to test common secnarios. 
This is built by F5 Business Development organization.

New Use Cases will be added periodically to provide additional senarios for BIG-IP Modules.

Workflow
--------

- Provisioner infrastructure using the F5 provisioner
- Run use cases using the infrastucture above

Goal
----

With F5 Automation provisioner and these scenario use cases, users can/will be able to

- Test common deployment scenarios through Automation with Ansible
- Fork instances of code to develop their own plugins and automation playbooks 
- Provide feedback on existing and new use cases that are relevant to everyday work

How to use
----------

Follow `F5 Ansible AWS Provisioner <https://github.com/f5alliances/f5_provisioner>`_ for
detailed steps to spin up and tear down the sandbox infrastructure

1. Login to the Ansible Host (**studentX-ansible**) provided by the F5 Ansible AWS Provisioner

   The Workbench information that is stored in a local directory named after the workshop after the provisioner is run

   - Example: <<workshop_name>>/instructor_inventory.txt

   Sample inventory.txt file:

   .. code::

      [all:vars]
      ansible_port=22

      [student1]
      student1-ansible ansible_host=34.219.251.xxx ansible_user=centos #Ansible host/control node
      student1-f5 ansible_host=52.39.228.xxx ansible_user=admin        #BIG-IP
      student1-host1 ansible_host=52.43.153.xxx ansible_user=centos    #Backend application server1
      student1-host2 ansible_host=34.215.176.xxx ansible_user=centos   #Backend application server2

2. Download the f5_ansible_use_cases Repo on the Ansible host
   
   - IP: Ansible control node IP from the inventory.txt file
   - username: studentx
   - password: provided while running the provisioner in f5_vars.yml

   .. code::

      ssh studentx@34.219.251.xxx
      cd ~/
      git clone https://github.com/f5alliances/f5_ansible_use_cases.git

   .. image:: images/Github-960.gif

.. note::

   The repo has been cloned to the ansible control node.
   Browse through readme of each use case in the next section to execute the playbooks

3. Login to the BIG-IP (**studentX-f5**) provided by the F5 Ansible AWS Provisioner
   
   Sample entry in inventory file: **student1-f5 ansible_host=52.39.228.xxx**
   
   - IP: BIG-IP from the inventory.txt file
   - Port: 8443
   - username: admin
   - password: provided while running the provisioner in f5_vars.yml
   
   .. code::
   
      https://52.39.228.xxx:8443
	  
.. note::

   Keep the BIG-IP login handy to login and validate configuration when use cases are executed
   
Support
-------

This project is a community effort to promote Network and Security automation and is maintained by F5 Business Development (BD). 
For anyfeature requests or issues, feel free to open an `issue <https://github.com/f5alliances/f5_ansible_use_cases/issues>`_
and we will give our best effort to address it.

.. note::

   Need help with automating use cases not present here - `Open a request <https://github.com/f5alliances/f5_ansible_use_cases/issues>`_
   
.. toctree::
   :glob:
   :maxdepth: 2
   :hidden:

   01-deploy-redirect-readme.rst
   02-certificate-replacement-readme.rst
   03-waf-policy-manipulation-readme.rst
   04-enable-disable-pool-members-readme.rst
   05-install-as3-readme.rst