---
layout: default
title: Persistent Storage
parent: The Basics
nav_order: 9
---

# Storage on Staas.io

Our stack storage is seperated into 2 categories
- Ephemera storage
- Persistent storage

## Ephemera storage
- Separated from each running container
- Life cycle  depent on stacks' running container lifetime
- Soft limit to 1GB per instance
- Could be use as high throuhput temporary file cache (Wordpress)
- Depent on base container that your stack is build from
- Not suitable for storing session, distributed data, persistent data

## Persistent storage
Based on Cloud native distributed block storage

- The storage is mounted to specified path depent on your stack plarforms.
  * Example: 
    * In Node.js `/mnt`
    * In Wordpress `/var/www/html`
- In Database stack, the mounted path is fixed into necessary folder and could not be changed
- Hard limit base on stack's package
- Persistent and synced between underlayer replicas
- Backup and point in time restore available accross physiscal regions & provider
- UI access via Filemanager. The mounted path is virtually set for web display and always view as `/data` folder.
- If your stack have Persistent Storage available, any restart / deployment / migrate action would have a minor downtime up to 5 minutes.
- The persistent storage is Rollback enable via Web Dashboard to any point in time. The rollback process will require your stack to be offline for approx 5-10 minutes depent on how big your current storage is.