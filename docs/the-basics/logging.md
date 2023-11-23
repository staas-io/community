---
layout: default
title: Logging
parent: The Basics
nav_order: 6
---

# Logging on Staas.io

## Recent Logs
Staas.io give user access to all containers logs via API. 

Example:
- https://www.staas.io/dashboard/stack_log/?id=scratchletter557&fullstack=true&since=86400&tail=1000&timestamps=false&format=html&wrap=true&refresh=30

Parameters:
- id: Joi.string().required(), stack id
- tail: Joi.number().integer().positive().max(1e6).optional().default(1000), log records limit
- since: Joi.number().integer().positive().max(60*60*24*7).optional().default(60*60), since period from now, by second
- end: Joi.date().timestamp().optional(), end period from now, by second
- timestamps: Joi.boolean().optional().default(true), show/hide timestamps
- format: Joi.string().optional().valid('plain', 'json', 'html').default('plain'), response format
- fullstack: Joi.boolean().optional().default(false), show all containers log or main app container only
- reverse: Joi.boolean().optional().default(false), show logs in reversed order
- label_inst: Joi.boolean().optional().default(true), show/hide label for each container instance


## Action Logs

Example:
- https://www.staas.io/dashboard/stack_log/?id=scratchletter557&action_log=true&action_log_url=s3%3A%2F%2Fstack%2Fconfig%2Fstaas%2Fadmin%2Fscratchletter557%2Flog%2Fstack-apply-2023-11-08-04%3A39%3A48.log

Parameters:
- id: Joi.string().required(), stack id
- format: Joi.string().optional().valid('plain', 'json', 'html').default('plain'), response format
- action_log: Joi.boolean().optional().default(false), get action log only
- action_log_url: Joi.string().uri().optional(), id of action log, if this parameter is missing the last action log is returned


## Writing to Your Log
Your logs capture anything your stack writes to standard out (stdout) or standard error (stderr).

In Node.js
```js
console.log(`Hello world`);
```

In Ruby:
```ruby
puts "Hello, logs!"
```

In Java:
```java
System.err.println("Hello, logs!");
System.out.println("Hello, logs!");
```

The same holds true for all other supported stack.
