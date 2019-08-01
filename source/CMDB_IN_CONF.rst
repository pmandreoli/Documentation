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

CMDB configuration
------------------
1. login in cmdb VM
2. create a directory called **cmdb-data**
3. Compile and move in  the following 3 .json files:

*image.json*

.. code:: json

 
  {
     "type": "image",
     "data": {
         "image_id": "8f667fbc-40bf-45b8-b22d-40f05b48d060",
         "image_name": "RECAS-BARI-ubuntu-16.04",
         "architecture": "x86_64",
         "type": "linux",
         "distribution": "ubuntu",
         "version": "16.04",
         "service": "service-RECAS-BARI-openstack"
     }
  }
  

*provider.json*

.. code:: json
    
   {
      "_id": "provider-RECAS-BARI",
      "data": {
          "name": "RECAS-BARI",
          "country": "Italy",
          "country_code": "IT",
          "roc": "NGI_IT",
          "subgrid": "",
          "giis_url": "ldap://cloud-bdii.recas.ba.infn.it:2170/GLUE2DomainID=RECAS-BARI,o=glue",
          "owners": [ "marcoantonio.tangaro@ba.infn.it" ]
      },
      "type": "provider"
   }
 

*service.json*

.. code:: json

   {
      "_id": "service-RECAS-BARI-openstack",
      "data": {
          "service_type": "eu.egi.cloud.vm-management.openstack",
          "endpoint": "https://cloud.recas.ba.infn.it:5000/v3",
          "provider_id": "provider-RECAS-BARI",
          "region": "recas-cloud",
          "sitename": "RECAS-BARI",
          "hostname": "cloud.recas.ba.infn.it",
          "type": "compute"
      },
      "type": "service"
   }
     
    
    
4. run the cmdb-add-data.sh in order to add image, provider, service, to CMDB.

*cmdb-add-data.sh*

.. code:: bash
 
   #!/bin/bash
   
   source /etc/cmdb/.cmdbenv
   
   if [[ -z "$CMDB_CRUD_USERNAME" ]]; then
   echo ENV variable CMDB_USER not set
   exit 1
   fi
   
   if [[ -z "$CMDB_CRUD_PASSWORD" ]]; then
   echo ENV variable CMDB_PASSWORD not set
   exit 1
   fi
   
   if [[ -z "$1" ]]; then
   echo "
   usage: $0 <json>
   "
   exit 1
   fi
   
   curl -X POST http://$CMDB_CRUD_USERNAME:$CMDB_CRUD_PASSWORD@localhost:5984/indigo-cmdb-v2 -H "Content-Type: application/json" -d@$1

5. Control on couchDB if your configuration has been uploaded accessing it from browser.
        
.. figure:: _static/cmdb_config.png
   :scale: 50%
   :align: center

.. centered:: couchDB after configuration process, containing image, provider and service       
       
       
       
