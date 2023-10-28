---
layout: default
title: Deploying with Git
parent: The Basics
nav_order: 2
---

# Deploying with Git
<!-- - Master branch
- Control branch (build/deploy)
- Github repo binding (optional -->

Staas.io simplifies application deployments by integrating seamlessly with Git, the widely used version control system.

Git is a distributed version control system that tracks changes in any set of computer files, usually used for coordinating work among programmers who are collaboratively developing source code during software development.

This article serves as a guide, detailing how to deploy code effortlessly using Git and Staas.io Git remotes. By following these steps, you can efficiently manage your application deployments, making the process straightforward and accessible even for those with limited Git expertise.


## Installing Git

You must have Git to deploy to Staas.io with Git. Here is the official guide for [Git installation instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

Before you can deploy your app to Staas.io, your code must be a valid Git repository.
Here's how to initialize a Git repository for an app in `myapp` directory:
```shell
$ cd myapp
$ git init
Initialized empty Git repository in .git/
$ git add .
$ git commit -m "init commit"
[main (root-commit) 7155318] init commit
 2 files changed, 1 insertion(+)
 create mode 100644 app.py
 create mode 100644 readme.md
```

## Create a Staas.io Remote

Git remotes are repository versions stored on external servers. You deploy your app by pushing its code to a Staas.io remote linked to your application.

While deploying your stack to Staas.io, you will need to add Staas.io's remote to your git repository:
```shell
$ git remote add staas git@git.staas.io:<your_staas_username>/<your_stack_name>.git
```

The correct command will be displayed on your stack's dashboard when you click on the [GIT](){: .btn .btn-purple .ml-2 } button. Here's how it looks like:
<!-- <image> -->

After you have run the command, your repository will have 2 remotes: `origin` and `staas`.
To check your remote, use the command `git remote -v` and you'll get something similar to this:
```shell
$ git remote -v
origin  git@github.com:staas-io/hello-staas.git (fetch)
origin  git@github.com:staas-io/hello-staas.git (push)
staas   git@git.staas.io:staas-username/stackname1234.git (fetch)
staas   git@git.staas.io:staas-username/stackname1234.git (push)
```

## Deploying Your Code

To deploy your app on Staas.io, simply use the git `push` command to push code from your local repository's `master` branch to your Staas.io remote. For instance:
```shell
$ git push -f staas master master:deploy
```

### Master Branch

Staas.io exclusively deploys code pushed to the `master` branches of the remote repository. Pushing code to other branches of the staas remote has no impact on the deployment process.

If you want to deploy code from another branch other than `master`, you might want to change the push command to this:
```shell
$ git push -f staas testbranch:master testbranch:deploy
```
The command above pushes code from `testbranch` to the Staas.io's 2 remotes `master` and `deploy` and build and deploy from your code from the `master` branch.

### Deploy Branch

As you might have noticed, we have `master:deploy` in the end of Staas.io's deploy command.
This part of the command means that you want to update the `deploy` branch on the remote repository `staas` **with the changes from your local `master` branch**. It effectively syncs your local `master` branch with the `deploy` branch on the remote repository `staas`.

In Staas.io, we use `deploy` branch as a control branch. It acts like a trigger mechanism for building and deploying your app. The reason for this is that we want you to have a separation of source branch and the deploy branch. You don't have to worry about mantaining the code in another branch other than your `master` branch.


## Github Binding (Optional)

Staas.io offers another way of deploying your application via Github Binding. When you have binded your Github account with Staas.io, Staas.io can use [Github's webhooks](https://docs.github.com/en/webhooks) to read and build directly from changes in your repository.

This method only works with your public repositories.

### Bind your Github account with Staas.io


### Build your Application via Github Binding

Step 1: Select repo to bind -> Press [BIND](){: .btn .btn-purple .ml-2 }

Step 2:
Instead of adding another remote (e.g. `staas`) to your code, binding allows you to trigger staas build by pushing to a branch named `staas` to the remote `origin` in your own repository.

Another major difference of this method is that Staas.io will build your application with the source code from the branch `staas` instead of `master`.

Assuming you are currently on your `master` branch, the example steps to trigger the build are:
```shell
$ cd hello-github-binding
$ git push -f origin master:staas
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 12 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 535 bytes | 535.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (4/4), completed with 2 local objects.
remote:
To github.com:staas-io/hello-github-binding.git
 * [new branch]      master -> staas
```

If your code has been setup correctly, the build process start immediately.
Note: This method doesn't support displaying console logs like the `staas` remote approach.

