---
layout: default
title: Logging
parent: The Basics
nav_order: 6
---

# Logging on Staas.io

Logging is a crucial aspect of managing and monitoring applications, providing insights into their behavior, performance, and potential issues.
Staas.io offers robust logging features to enhance your application management experience.

## Build Logs


## Runtime Logs

### Writing to Your Log
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

In Python:
```python
print("Hello, logs!")
```

The same holds true for all other supported stack.


### View Logs
You can view your logs through your stack's dashboard.
Staas.io give user access to all containers logs via API.

Example:
```
https://www.staas.io/dashboard/stack_log/?id=scratchletter557&fullstack=true&since=86400&tail=1000&timestamps=false&format=html&wrap=true&refresh=30
```

#### Parameters:

- **`id`** (string, _required_) 
  - Stack ID: Identifies the stack for which logs are requested.

- **`tail`** (number, _optional_, defaults to 1,000, maximum 1,000,000) 
  - Log Records Limit: Limits the number of log records to retrieve.

- **`since`** (number, _optional_, defaults to 3,600, maxixum `3600x24x7`) 
  - Since Period: Specifies the beginning time from now, in seconds, to retrieve logs.

- **`end`** (number, _optional_) 
  - End Period: Specifies the end time from now, in seconds, to retrieve logs.

- **`timestamps`** (boolean, _optional_, defaults to `true`) 
  - Show/Hide Timestamps: Indicates whether to show or hide timestamps in the log entries.

- **`format`** (string, _optional_, defaults to "`plain`") 
  - Response Format: Specifies the format of the log entries in the response. Available options: "`plain`", "`json`", "`html`"

- **`fullstack`** (boolean, _optional_, defaults to `false`) 
  - Show All Containers Log: Determines whether to show logs for all containers or only the main application container.

- **`reverse`** (boolean, _optional_, defaults to `false`) 
  - Show Logs in Reversed Order: Specifies whether to display logs in reverse order.

- **`label_inst`** (boolean, _optional_, defaults to `true`) 
  - Show/Hide Label for Each Container Instance: Indicates whether to show or hide labels for each container instance.

Feel free to adjust these parameters based on your log retrieval requirements. If you have any questions or need further assistance, refer to the Staas.io documentation or reach out to our support team.


<!-- Parameters:
- `id`: Joi.string().required(), stack id
- `tail`: Joi.number().integer().positive().max(1e6).optional().default(1000), log records limit
- `since`: Joi.number().integer().positive().max(60*60*24*7).optional().default(60*60), since period from now, by second
- `end`: Joi.date().timestamp().optional(), end period from now, by second
- `timestamps`: Joi.boolean().optional().default(true), show/hide timestamps
- `format`: Joi.string().optional().valid('plain', 'json', 'html').default('plain'), response format
- `fullstack`: Joi.boolean().optional().default(false), show all containers log or main app container only
- `reverse`: Joi.boolean().optional().default(false), show logs in reversed order
- `label_inst`: Joi.boolean().optional().default(true), show/hide label for each container instance -->


## Action Logs

Action logs are ...

Example:
```
https://www.staas.io/dashboard/stack_log/?id=scratchletter557&action_log=true&action_log_url=s3%3A%2F%2Fstack%2Fconfig%2Fstaas%2Fadmin%2Fscratchletter557%2Flog%2Fstack-apply-2023-11-08-04%3A39%3A48.log
```


#### Parameters:

- **`id`** (string, _required_) 
  - Stack ID: Identifies the stack for which action logs are requested.

- **`format`** (string, _optional_, defaults to "`plain`") 
  - Response Format: Specifies the format of the action log entries in the response. Available options: "`plain`", "`json`", "`html`"

- **`action_log`** (boolean, _optional_, defaults to `false`) 
  - Get Action Log Only: Indicates whether to retrieve only the action log.

- **`action_log_url`** (string, URI, _optional_) 
  - ID of Action Log: If this parameter is missing, the last action log is returned. Provides the ID for a specific action log.


<!-- Parameters:
- id: Joi.string().required(), stack id
- format: Joi.string().optional().valid('plain', 'json', 'html').default('plain'), response format
- action_log: Joi.boolean().optional().default(false), get action log only
- action_log_url: Joi.string().uri().optional(), id of action log, if this parameter is missing the last action log is returned -->
