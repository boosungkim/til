# HTTP Status Codes

I've been working in backend for a few months now, and I feel like it's about time I properly learn/memorize what different status codes mean in the HTTP protocol. I know what the general ranges refer to, but not knowing specific numbers have hindered my design choices a few times in the recent weeks.

## High-level ranges
There are 5 high-level ranges 

- 100 ~ 199: Informational responses
- 200 ~ 299: Successful responses
- 300 ~ 399: Redirection messages
- 400 ~ 499: Client error responses
- 500 ~ 599: Server error responses

## Informational responses (100 ~ 199)
- 100 Continue: Indicates that the client should continue the request OR ignore the response if the request is already finished.
- 101 Switching Protocols: Indicates the protocol the server is switching to.
- 102 Processing: Indicates the request was received by the server, but no status was available at the time.
- 103 Early Hints: Allows the user to start preloading resources while the server prepares a response.

## Successful responses (200 ~ 299)
- 200 OK: Indicates the request succeeded.
- 201 Created: Indicates the request succeeded, and a new resource was created as a result.
- 202 Accepted: Indicates the request was received but has not yet been acted upon (noncommittal).
- 203 Non-Authoritative Information: Indcates the returned metadata is not exactly the same as is available from the origin server (usually backups).
- 204 No Content: Indicates there is no content to send for this request.
- 205 Reset Content: Informs the user agent to reset the document which sent this request.
- 206 Partial Content: Response to range requests.

## Redirection message (300 ~ 399)
- 300 Multiple Choices
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 305 Use Proxy
- 306 Unused
- 307 Temporary Redirect
- 308 Permanent Redirect

## Client error respones (400 ~ 499)
- 400 Bad Request: Indicates a client-side error, like malformed/invalid request.
- 401 Unauthorized: Indicates "unauthenticated," meaning the client should authenticate itself.
- 403 Forbidden: Indicates the client does not have access rights to the content.
- 404 Not Found: Indicates the server cannot find the requested resource (i.e. URL is not recognized, the file DNE in storage).
- 405 Method Not Allowed: Indicates the target resource does not support the request, like an API not allowing DELETE on a resource.
- 408 Request Timeout
- 409 Conflict
- 412 Precondition Failed: For conditional requests.
- 413 Content Too Large
- 415 Unsupported Media Type
- 416 Range Not Satisfiable
- 418 I'm a teapot (?)
- 421 Misdirected Request
- 428 Precondition Required: For conditional requests.
- 429 Too Many Requests: Rate limiting for too many requests.

## Server error responses (500 ~ 599)
- 500 Internal Server Error: Indicates the server encountered a un-handlable situation (generic, so try to use another code).
- 501 Not Implemented: Indicates the request is not supported by the server. GET and HEAD should be supported by the server and hence should not return this code.
- 502 Bad Gateway: Indicates an invalid response while handling a request.
- 503 Service Unavailable: Indicates the server is not ready to handle the request.
- 504 Gateway Timeout: Indicates the server could not get a response in time.

## Resources
- Mozilla: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status