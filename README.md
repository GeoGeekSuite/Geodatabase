Geodatabase
=========

Ansible role to deploy a PostGIS database to a Kubernetes Cluster.

Requirements
------------

This role is intended to work with the deployment script of GeoGeekSuite.
It requires a running Kubernetes cluster.

Role Variables
--------------

manifest_folder
gisnamespace
geodatabase:
  dbname
  dbadmin
  dbpw
  dbpwe
  container_image
  container_version

Dependencies
------------


Example Playbook
----------------

---
- hosts: local
  vars_prompt:
    - name: password
      prompt: Set an internal password?
  vars:
    manifest_folder: ~/geogeek_manifests
    gisnamespace: gis
    geodatabase:
      dbname: postgres
      dbadmin: postgres
      dbpw: '{{ password }}'
      dbpwe: '{{ password | b64encode }}'
      container_image: kartoza/postgis
      container_version: 14-3.3
    project_folder: '~/Projects/GeoGeekSuite'
    storage_base: '{{ project_folder }}/data'
    storage: 
    - name: postgres 
      type: local 
      path: '{{ storage_base }}/postgres'
      size: 5Gi
  roles:
  - { role: postgres,
        tags: postgres }

License
-------

Apache, Version 2.0

Author Information
------------------

Marco Bradtke
www.geogeeksuite.com
