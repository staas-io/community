---
layout: default
title: Entry Points
parent: The Basics
nav_order: 5
---

# Entry Points

Running your application on Staas.io generally requires minimal changes.
One essential requirement is specifying which parts of your application are executable on the platform.

An entry point or Procfile is a configuration file that specifies the commands that are executed by the app on startup. It provides instructions to Staas.io on how to run the application. The Procfile is particularly important because it tells Staas.io which parts of your application are runnable.

For example, if you have a web application built with Node.js, your Procfile might look like this:
```
web: node server.js
```

Or for Python, it could look like this:
```
web: python manage.py runserver 0.0.0.0:8000
```

In this example, `web` is the process type, and `node server.js` or `python manage.py runserver 0.0.0.0:8000` are the commands that starts your Node.js/Django server. When you deploy your application to Staas.io, it reads the Procfile and knows how to start your app.

<!-- The Procfile can include various process types, each with its corresponding command. Besides the web process, you might have worker processes, background tasks, or other components of your application defined in the Procfile. This flexibility allows you to specify the exact behavior of your application on the Staas.io platform. Properly configuring the Procfile ensures that Staas.io can manage your app correctly, making it a fundamental aspect of deploying applications on the Staas.io platform. -->