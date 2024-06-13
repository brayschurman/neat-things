# REST
REpresentational State Transfer

- an architectural style for providing standards between computer systems
- implementation of **client** and **server** are done independently
	- code in each can be changed and other is unaffected
	- clients make requests, servers send responses
- **stateless**, components of system don't need to know about each other, just the paradigms for sending data

## Making Requests
- an HTTP verb (GET, POST, PUT, DELETE)
- a header
- a path

## Sending Responses
- content type
- response code

### Response Codes

| Status Code | Description           | Category     |
| ----------- | --------------------- | ------------ |
| 200         | OK                    | Success      |
| 201         | Created               | Success      |
| 202         | Accepted              | Success      |
| 204         | No Content            | Success      |
| 301         | Moved Permanently     | Redirection  |
| 302         | Found                 | Redirection  |
| 303         | See Other             | Redirection  |
| 304         | Not Modified          | Redirection  |
| 307         | Temporary Redirect    | Redirection  |
| 308         | Permanent Redirect    | Redirection  |
| 400         | Bad Request           | Client Error |
| 401         | Unauthorized          | Client Error |
| 403         | Forbidden             | Client Error |
| 404         | Not Found             | Client Error |
| 405         | Method Not Allowed    | Client Error |
| 409         | Conflict              | Client Error |
| 410         | Gone                  | Client Error |
| 429         | Too Many Requests     | Client Error |
| 500         | Internal Server Error | Server Error |
| 501         | Not Implemented       | Server Error |
| 502         | Bad Gateway           | Server Error |
| 503         | Service Unavailable   | Server Error |
| 504         | Gateway Timeout       | Server Error |
