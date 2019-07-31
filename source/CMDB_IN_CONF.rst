CMDB and CPR installation and configuration
===========================================

Setting up CMDB role
--------------------

1. Create and edit cmdb.yaml in **group_vars** that contain all the following variables:

.. highlight:: none

::
 
 cmdb_crud_password: CMDBpassword
 cmdb_oidc_userinfo: https://<proxy_HOSTNAME>/userinfo

                   
.. highlight:: default

Run the role
------------

* run the cmdb role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-cmdb.yml``
* run the cpr role using *ansible-playbook* with input ``indigopass-deploy/indigopaas-deploy/ansible/playbooks/deploy-cpr.yml``

