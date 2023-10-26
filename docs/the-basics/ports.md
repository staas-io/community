---
layout: default
title: Ports
parent: The Basics
nav_order: 3
---

# Ports

Ports are virtual places within an operating system where network connections start and end. They help computers sort the network traffic they receive.

Ports are standardized across all network-connected devices, with each port assigned a number.
While IP addresses enable messages to go to and from specific devices, port numbers allow targeting of specific services or applications within those devices.

Your application may be listening on a port for incomming requests. When you run your application locally, you usually access it in your web browser through a URL like: `http://localhost:5000/`. The number after the colon is known as a port number. It can be any number between 1024 and 65535.

Some high level frameworks take care of this for you. Sometimes you have to define this yourself. It is recommended to get this number from the environment variables.

For example, in Python:
```python
port = os.environ.get("PORT", 5000)
app.run(host="0.0.0.0", port=int(port))
```

Or in Node.js, there is typically a file named `server.js` or `server.ts`:
```js
const hostname = "0.0.0.0";
const port = process.env.port || 5000;

app.listen(port, hostname, () => {
  console.log(`Listening on http://${hostname}:${port}/`);
});
```

In order to receive traffic from the internet, your Staas.io's server must also have this port opened as well.

## Ports in Staas.io

Staas.io lets you set your listening port number through the Dashboard, in the Operation section.

In your stack's dashboard, you can see an **Operation** section with a sub-section named **Environment** just below.

Click on the checkbox "**I understand that reveal this sensitive information might unintentional leak the security of my stacks**" to review your system's environment variables.
![](../../assets/images/the-basics/environment-vars.jpg)

Now you can update the `PORT` variable to match with the port number of your application. Whenever you change your port number, you must update this variable as well.

### Listening Host

A common issue arises when applications are configured to accept connections only from `localhost` instead of the broader internet.
To address this problem, if your code restricts connections to `localhost`, modify the hostname value to either `0.0.0.0` or `[::]`.

Different frameworks may require you to change command used to start your application:
- For Gunicorn applications, use: `gunicorn --bind 0.0.0.0:8000 myproject.wsgi`
- For Fastify applications, use: `fastify start --address 0.0.0.0`

