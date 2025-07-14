---
id: 20
date: 2025-07-14T00:00:00Z
title: "HTTP Status Codes Cheatsheet"
author: "Jeremy Novak"
summary: "Reference for HTTP status codes"
slug: http-status-codes-cheatsheet
tags:
  - http
  - web
  - api
published: true
---

# HTTP Status Codes Cheatsheet

---

## 1xx Informational Responses

| **Code** | **Name** | **Description** |
|----------|----------|-----------------|
| 100 | Continue | The server has received the request headers and the client should proceed to send the request body |
| 101 | Switching Protocols | The requester has asked the server to switch protocols and the server has agreed |
| 102 | Processing | The server has received and is processing the request, but no response is available yet |
| 103 | Early Hints | Used to return some response headers before final HTTP message |

---

## 2xx Success

| **Code** | **Name** | **Description** |
|----------|----------|-----------------|
| 200 | OK | Standard response for successful HTTP requests |
| 201 | Created | The request has been fulfilled and a new resource has been created |
| 202 | Accepted | The request has been accepted for processing, but processing has not been completed |
| 203 | Non-Authoritative Information | The server successfully processed the request but is returning modified information |
| 204 | No Content | The server successfully processed the request and is not returning any content |
| 205 | Reset Content | The server successfully processed the request, asks the requester to reset the document view |
| 206 | Partial Content | The server is delivering only part of the resource due to a range header sent by the client |
| 207 | Multi-Status | The message body contains an XML message and can contain multiple response codes |
| 208 | Already Reported | The members of a DAV binding have already been enumerated in a previous reply |
| 226 | IM Used | The server has fulfilled a request for the resource with one or more instance-manipulations applied |

---

## 3xx Redirection

| **Code** | **Name** | **Description** |
|----------|----------|-----------------|
| 300 | Multiple Choices | Multiple options for the resource that the client may follow |
| 301 | Moved Permanently | The requested resource has been permanently moved to a new URI |
| 302 | Found | The requested resource resides temporarily under a different URI |
| 303 | See Other | The response can be found under a different URI using GET method |
| 304 | Not Modified | The resource has not been modified since the version specified by request headers |
| 305 | Use Proxy | Deprecated - The requested resource must be accessed through the proxy given by the Location field |
| 307 | Temporary Redirect | The request should be repeated with another URI; however, future requests should still use the original URI |
| 308 | Permanent Redirect | The request and all future requests should be repeated using another URI |

---

## 4xx Client Errors

| **Code** | **Name** | **Description** |
|----------|----------|-----------------|
| 400 | Bad Request | The server cannot process the request due to client error (e.g., malformed syntax) |
| 401 | Unauthorized | Authentication is required and has failed or has not been provided |
| 402 | Payment Required | Reserved for future use (originally intended for digital payment systems) |
| 403 | Forbidden | The server understood the request but refuses to authorize it |
| 404 | Not Found | The requested resource could not be found on the server |
| 405 | Method Not Allowed | The request method is not supported for the requested resource |
| 406 | Not Acceptable | The requested resource is only capable of generating content not acceptable according to Accept headers |
| 407 | Proxy Authentication Required | The client must first authenticate itself with the proxy |
| 408 | Request Timeout | The server timed out waiting for the request |
| 409 | Conflict | The request could not be processed due to a conflict with the current state of the resource |
| 410 | Gone | The requested resource is no longer available and will not be available again |
| 411 | Length Required | The request did not specify the length of its content, which is required |
| 412 | Precondition Failed | The server does not meet one of the preconditions specified in the request headers |
| 413 | Payload Too Large | The request is larger than the server is willing or able to process |
| 414 | URI Too Long | The URI provided was too long for the server to process |
| 415 | Unsupported Media Type | The request entity has a media type which the server does not support |
| 416 | Range Not Satisfiable | The client has asked for a portion of the file, but the server cannot supply that portion |
| 417 | Expectation Failed | The server cannot meet the requirements of the Expect request-header field |
| 418 | I'm a teapot | This code was defined in 1998 as an April Fools' joke (RFC 2324) |
| 421 | Misdirected Request | The request was directed at a server that is not able to produce a response |
| 422 | Unprocessable Entity | The request was well-formed but unable to be followed due to semantic errors |
| 423 | Locked | The resource being accessed is locked |
| 424 | Failed Dependency | The request failed due to failure of a previous request |
| 425 | Too Early | The server is unwilling to risk processing a request that might be replayed |
| 426 | Upgrade Required | The client should switch to a different protocol |
| 428 | Precondition Required | The origin server requires the request to be conditional |
| 429 | Too Many Requests | The user has sent too many requests in a given amount of time (rate limiting) |
| 431 | Request Header Fields Too Large | The server is unwilling to process the request because header fields are too large |
| 451 | Unavailable For Legal Reasons | The server is denying access to the resource due to legal demands |

---

## 5xx Server Errors

| **Code** | **Name** | **Description** |
|----------|----------|-----------------|
| 500 | Internal Server Error | A generic error message when the server encounters an unexpected condition |
| 501 | Not Implemented | The server does not recognize the request method or lacks the ability to fulfill it |
| 502 | Bad Gateway | The server was acting as a gateway or proxy and received an invalid response |
| 503 | Service Unavailable | The server is currently unavailable (overloaded or down for maintenance) |
| 504 | Gateway Timeout | The server was acting as a gateway or proxy and did not receive a timely response |
| 505 | HTTP Version Not Supported | The server does not support the HTTP protocol version used in the request |
| 506 | Variant Also Negotiates | Transparent content negotiation for the request results in a circular reference |
| 507 | Insufficient Storage | The server is unable to store the representation needed to complete the request |
| 508 | Loop Detected | The server detected an infinite loop while processing the request |
| 510 | Not Extended | Further extensions to the request are required for the server to fulfill it |
| 511 | Network Authentication Required | The client needs to authenticate to gain network access |

---

## Common Use Cases

### API Development
- **200 OK**: Successful GET, PUT, or PATCH request
- **201 Created**: Successful POST request that creates a resource
- **204 No Content**: Successful DELETE request
- **400 Bad Request**: Invalid request data or parameters
- **401 Unauthorized**: Missing or invalid authentication
- **403 Forbidden**: Authenticated but not authorized
- **404 Not Found**: Resource doesn't exist
- **409 Conflict**: Resource state conflict (e.g., duplicate entry)
- **422 Unprocessable Entity**: Validation errors
- **429 Too Many Requests**: Rate limit exceeded

### Web Applications
- **301 Moved Permanently**: URL has permanently changed
- **302 Found**: Temporary redirect
- **304 Not Modified**: Cached resource is still valid
- **503 Service Unavailable**: Server maintenance or overload

### Authentication & Authorization
- **401 Unauthorized**: No valid authentication credentials
- **403 Forbidden**: Valid credentials but insufficient permissions
- **407 Proxy Authentication Required**: Proxy requires authentication

### Content Negotiation
- **406 Not Acceptable**: Cannot produce response matching Accept headers
- **415 Unsupported Media Type**: Request body format not supported

---

## Best Practices

1. **Use appropriate status codes** - Don't use 200 for errors
2. **Include error details** - Provide meaningful error messages in response body
3. **Be consistent** - Use the same codes for similar situations across your API
4. **Document your codes** - List which status codes your API returns
5. **Don't expose sensitive information** - Be careful with error messages in production
