Virtual Machine deployment 
==============================================

The INDIGO-DataCloud softwares are dockerized and each one run on a specific VM(Fig.1)

.. figure:: _static/laniakea_pass_container_VM.png
   :scale: 80%
   :align: center

.. centered:: Fig.1: PaaS component architecture scheme



On the Openstack tenant the virtual machines that will contain the Laniakea INDIGO-DataCloud services has to be created (table.1)
Default caracteristic:

* SO = Ubuntu 16.04
* Open ports = 22,80  

.. centered:: necessary virtual machines complete with minimum requirements for the installation of Laniakea service

.. csv-table::
   :header: "Service", "RAM", "vCPU", "Storage", "open ports", "net"
   :widths: auto
   :file: ./table_VMS.csv



.. note:: The vm_master, as well as hosting the proxy server, will be utilized as control virtual machine from this vm all the services will be installed using `Ansible <https://www.ansible.com/>`_


