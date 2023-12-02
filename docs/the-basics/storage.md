---
layout: default
title: Storage
parent: The Basics
nav_order: 10
---

# Storage on Staas.io

In Staas.io, storage is a fundamental element that ensures your data is securely stored and readily accessible.
Whether you're managing files, databases, or other application-related data, Staas.io's storage solutions are designed to simplify the storage process, providing reliability and efficiency.
Explore the seamless integration of storage features within Staas.io, offering a hassle-free experience for preserving and managing your crucial data.

Our stack storage is seperated into 2 categories:

- Ephemera storage
- Persistent storage

## Ephemera storage
Ephemeral storage refers to a temporary and short-lived form of storage that is closely tied to the lifecycle of your application's containers.
Unlike persistent storage, which retains data even when the application is stopped or restarted, ephemeral storage is designed for transient data that doesn't need to persist beyond the current session.

Key Characteristics:
- Separated from each running container.
- Life cycle depends on the stack's running container lifetime.
- Soft limit to 1GB per instance.
- For performance optimization, it could be use as high throuhput temporary file cache (e.g. Wordpress stack).
- Not suitable for storing session, distributed data, persistent data.
- Availability depends on base container that your stack is build from.

**When deploying on Staas.io, your application is deployed on the emphemeral storage of the instance.**
Consider this information carefully when storing data in your application.

## Persistent storage
Persistent storage in Staas.io refers to a durable and long-lasting form of storage designed to retain data beyond the lifecycle of your application's containers.
Unlike ephemeral storage, which is temporary and tied to the runtime of the application, persistent storage ensures that data persists even when containers are stopped, restarted, or replaced.

Our Persistent Storage is based on Cloud native distributed block storage.
Cloud-native distributed block storage is a storage solution optimized for cloud environments and designed to meet the dynamic and scalable requirements of modern applications.

### Mount points
The storage is mounted to specified path depent on your stack plarforms.
For example: 
- In Node.js: `/mnt`
- In Wordpress: `/var/www/html`
- In Database stacks, the mounted path is fixed into necessary folders and could not be changed.

### Accessibility
Storage can be accessed via [File Manager]({% link docs/file-manager.md %}) UI.
The mounted path is virtually set for web display and always view as `/data` folder.

### Storage limit
Storage has a hard limit base on stack's package.

### Backup and Rollback
Your persistent storages are persistent and synced between underlayer replicas.

Backup and point in time restore available accross physiscal regions & providers.

If your stack have Persistent Storage available, any restart / deployment / migrate action would have a minor downtime up to 5 minutes.

The persistent storage is Rollback enable via Web Dashboard to any point in time.

The rollback process will require your stack to be offline for approx 5-10 minutes depent on how big your current storage is.

To see how you can restore your storage between snapshot, head over to [Backup Storage with Staas.io]({% link docs/the-basics/backup.md %}).
