## Status CODE

The common are:

- `200` OK: Standard response for successful HTTP requests. The actual response will depend on the request method used.
- `201` Created: The request has been fulfilled, resulting in the creation of a new resource.
- `202` Accepted: The request has been accepted for processing, but the processing has not been completed. The request might or might not be eventually acted upon, and may be disallowed when processing occurs
- `204` No Content: The server successfully processed the request and is not returning any content
- `301` Moved Permanently: This and all future requests should be directed to the given URI
- `400` Bad Request: The server cannot or will not process the request due to an apparent client error
- `401` Unauthorized: Similar to 403 Forbidden, but specifically for use when authentication is required and has failed or has not yet been provided.
- `403` Forbidden: The request was valid, but the server is refusing action. The user might not have the necessary permissions for a resource, or may need an account of some sort.
- `404` Not Found: The requested resource could not be found but may be available in the future. Subsequent requests by the client are permissible.
- `405` Method Not Allowed: A request method is not supported for the requested resource; for example, a GET request on a form that requires data to be presented via POST, or a PUT request on a read-only resource.
- `408` Request Timeout: The server timed out waiting for the request. According to HTTP specifications: "The client did not produce a request within the time that the server was prepared to wait. The client MAY repeat the request without modifications at any later time.
- `429` Too Many Requests: The user has sent too many requests in a given amount of time.
- `500` Internal Server Error: A generic error message, given when an unexpected condition was encountered and no more specific message is suitable.
