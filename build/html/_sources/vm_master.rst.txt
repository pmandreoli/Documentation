configure the control machine
=============================

In order to install every indigo software using the Ansible roles made avaiable by INDIGO the vm_master Ansible need to be installed and configured.



Ansible installation
####################

`Install Ansible <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>`_

Minimum version 2.1.2.0 recommended  2.8.3

Ansible configuration
#####################

the inventory file has to be populated wit the IP of the virtual machines tagged by name.
 

**1.** **inventory example**

.. code:: bash

   [iam]
   <VM_IAM IP>

   [im]
   <VM_IM IP>

   [cmdb]
   <VM_CMDB IP>

   [slam]
   <VM_SLAM IP>

   [cpr]
   <VM_CPR IP>

   [proxy]
   <VM_PROXY IP>

   [orchestrator]
   <VM_ORCHESTRATOR IP>

**2.** **Ansible role download**


| 2.1. Clone or download the role `indigopaas-deploy <https://github.com/indigo-dc/indigopaas-deploy/tree/devel>`_ devel branch.

| 2.2. Create the variable the directory **group_vars** in ``indigopaas-deploy/ansible/inventory/``. This directory will contain a .yml file containing the compulsory role vars for every component.

| e.g


|        group_vars/
|        ├── cmdb.yml
|        ├── im.yaml
|        ├── proxy.yml
|        └── slam.yaml


.. metti anche che i playbook installano i componenti su HTTPS usando LetSencrypt   
