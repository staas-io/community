---
layout: default
title: Enviroment
parent: The Basics
nav_order: 7
---

# Enviroment on Staas.io

Due the the cloud enviroment of Staas.io, enviroment play an important role for you to control your stack

- All the enviroment will be passed as Build Arguments when your stack is build
- All enviroment will be appllied when your stack is running
- You can edit enviroment one by one via our Web dashboard
- You can import/export stack enviroment by clicking in import/export icon in our dashboard 
- Due to the important of enviroment playing, they're could be updated during the Build / Deployment process, so normally you should avoid updating enviroment in parallel (such as multi tab, or when your stack is built and deployed) to avoid any conflict & missing without notice
- All enviroment variables should be on Capitalized and dont contain special/ nonvisible / non ascii character (NewLine, Color Format)
- Although we support complex enviroment value such as single line JSON, but it's not guaranteed for any special effect due to the vast support of building context

## Important enviroments

- PORT: Indicated main running application port
- NODEPORT: Indicated main public port for mostly database access
- FILEMANAGER_USERNAME
- FILEMANAGER_PASSWORD
- FILEMANAGER

## Read-only enviroments
- INTERNAL_SVC_HOST: Indicated private domain for your stack when your need to access it from another stack of same owner via private network
- ST4AS_COMMIT: Indicated hash commit of your built image form git repository
- ST4AS_BUILD_AT: Indicated the build time

## Custom enviroments
- NO_STORAGE: force remove persistent volume storage to give your stack ability to freely scale & running cross region
- COMMAND: overwrite starting command for your stack
- K8S_SUB_DIR: N/A yet