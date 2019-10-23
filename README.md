# ansible-role-shibboleth
Ansible galaxy role cesnet.shibboleth_sp that install and configure shibboleth SP

## Requirements


## Role variables
* shibboleth_hostname - Specify the hostname 
* shibboleth_sp_entity_id - Specify the entityId of Service provider

###### Followed options are only for the default attribute_map.xml template
* shibboleth_template_attribute_map_allow_urn_oid_attributes - Specify if default urn:oid attributes will be added to attribute map or not
* shibboleth_template_attribute_map_allow_urn_mace_attributes - Specify if default urn:mace attributes will be added to attribute map or not
* shibboleth_template_attribute_map_allow_schac_attributes - Specify if default schac attributes will be added to attribute map or not
* shibboleth_template_attribute_map_custom_attributes - Specify the custom attributes that will be added to attribute map
    * Example of structure:
  ```
  shibboleth_template_attribute_map_custom_attributes:
      - id: attributeId (REQUIRED)
        name: attributeName (REQUIRED)
        comment: Commnent (OPTIONAL)
        decoder: (OPTIPNAL)
          type: Decoder_type (REQUIRED if decoder is filled)
  ```

###### Change these options only if you use the default shibboleth2.xml template 
* shibboleth_template_sp_entity_id - Specify the entityId of Service provider
* shibboleth_template_remote_users - Specify the list of allowed items in REMOTE_USER
* shibboleth_template_attribute_prefix - Specify the attribute prefix
* shibboleth_template_idp_entity_id - Specify the entityId of Identity provider
* shibboleth_template_metadata_url - Specify the URL where the IdP metadata is available
* shibboleth_template_metadata_backup_file - Specify the name of backup file for metadata

## Available tags
* install
* configuration
* start
* stop

## Example playbook
```
- hosts: all
  remote_user: root
  vars:
    shibboleth_hostname: "sp.example.org"
    shibboleth_sp_entity_id: "https://{{ shibboleth_hostname }}/shibboleth"
    shibboleth_template_attribute_map_allow_urn_oid_attributes: true
    shibboleth_template_attribute_map_allow_urn_mace_attributes: true
    shibboleth_template_attribute_map_allow_schac_attributes: true
    shibboleth_template_attribute_map_custom_attributes: []
    shibboleth_template_sp_entity_id: "https://{{ shibboleth_hostname }}/shibboleth"
    shibboleth_template_remote_users:
        - eppn
    shibboleth_template_attribute_prefix: "AJP_"
    shibboleth_template_idp_entity_id: "https://idp.example.org/idp/shibboleth"
    shibboleth_template_metadata_url: "http://federation.org/federation-metadata.xml"
    shibboleth_template_metadata_backup_file: "metadata.xml"
  roles:
    - cesmet.shibboleth_sp
```