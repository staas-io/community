---
layout: default
title: Staas Fundamental Concepts
nav_order: 3
---

# Staas Fundamental Concepts

This section provides a basic and technical overview of the functioning of Staas.io.
It explains various concepts involved in the process of writing, configuring, deploying, and operating applications on the Staas.io platform.


## Defining an Application on Staas.io

At Staas.io, you can deploy, run, and manage applications created in programming languages like Ruby, Node.js, Java, Python, Clojure, Scala, Go, and PHP. You can even deploy popular databases and popular applications (e.g. WordPress) with just a few mouse clicks!

An application here refers to a package of source code written in one of these languages, possibly including a framework. It also includes a description of the dependencies required for the application to function. These dependencies guide a build system on which additional components are needed to build and run the application.

In simpler terms, an application on Staas.io consists of your written code and a list of what else is needed for it to work. The specific requirements vary based on the programming language used: Ruby employs a `Gemfile`, Python uses a `requirements.txt`, Node.js relies on `package.json`, Java utilizes `pom.xml`, and so on.

When you provide your application's source code and its dependency information, Staas.io can use this data to build and execute your application.

## Defining your Executable

Running your application on Staas.io typically requires minimal effort. One essential requirement is specifying which parts of your application are executable.

You need to explicitly state what can be executed. This is done through a text file called a `Procfile`, which accompanies your source code. In the `Procfile`, each line defines a process type which is a named command that can run within your built application. For instance:

```

```
<!-- 
Here, the Procfile specifies a 'web' process type with the corresponding command needed to run it (java -jar lib/foobar.jar $PORT). Similarly, it defines a 'queue' process type and its corresponding command. -->

Staas.io allows you to build, run, and scale applications consistently across various languages, utilizing both dependencies and the `Procfile`. The `Procfile` exposes the architectural aspects of your application and this enables independent scaling of each part of the application.

## Deploying your Applications

Staas.io leverages Git as the primary method to deploy applications, although there are alternative methods like using an API to transport your source code to Staas.io.

When you create an stack on Staas.io, it sets up a new Git remote, usually named `staas`, connected to your local Git repository.

Deploying your code is as straightforward as using the familiar `git push` command, but directed to the `staas` remote, assuming your current branch is `master`:

```shell
git push -f staas master master:deploy
```

## Building your Applications

When Staas.io gets your application source, it begins a building process specific to the programming language used. It involves fetching the specified dependencies and creating necessary assets, whether it's processing style sheets or compiling code.

For instance, if the build system receives a Python application, it might fetch dependencies listed in the `requirements.txt` file and generate files based on the asset pipeline. In the case of a Java application, it could fetch binary libraries using Maven, compile the source code along with these libraries, and create a JAR file for execution. These processes ensure that your application is properly compiled and ready to run on Staas.io.


## Running your Applications

With Staas.io, you have the ultimate control over the number of instances running for your applications, providing you with the flexibility to adjust the scale according to your needs.
This level of control is made possible through the Admin Control feature, accessible directly from your stack's dashboard.
Here, you can easily manage and configure the precise number of instances required at any given time, ensuring optimal performance and resource utilization.

<!-- Staas.io offers the flexibility to scale your applications both horizontally and vertically. Horizontal scaling involves adding more instances of your application to distribute the load, ensuring efficient performance during high traffic periods. Vertical scaling, on the other hand, means increasing the resources (such as CPU, RAM, or storage) of a specific server, enabling your application to handle larger individual tasks. With Staas.io, you have the capability to adjust your application's scale dynamically, ensuring seamless performance and responsiveness, regardless of varying demands and complexities. -->

## Logging and monitoring
