# HTTP methods descriptions

|    Method   | Description |
|-------------|-------------|
| **GET**     | Requests a representation of the specified resource. Requests using **GET** should only retrieve data.	| 
| **HEAD**	  | Asks for a response identical to a **GET** request, but without the response body. |
| **POST**	  | Submits an entity to the specified resource, often causing a change in state or side effects on the server. |
| **PUT**	  | Replaces all current representations of the target resource with the request payload. |
| **DELETE**  | Deletes the specified resource. |
| **PATCH**	  | Applies partial modifications to a resource. |
| **OPTIONS** | Describes the communication options for the target resource. |
| **CONNECT** | Establishes a tunnel to the server identified by the target resource. |
| **TRACE**   | Performs a message loop-back test along the path to the target resource. |

## GET

The **HTTP GET** method requests a representation of the specified resource. Requests using **GET** should only be used to request data (they shouldn't include data).

|                              |    |
|------------------------------|----|
| Request has body             | ❌ |
| Successful response has body | ✔️ |
| Safe                         | ✔️ |
| Idempotent                   | ✔️ |
| Cacheable                    | ✔️ |
| Allowed in HTML forms        | ✔️ |

## HEAD

The **HTTP HEAD** method requests the headers that would be returned if the **HEAD** request's URL was instead requested with the **HTTP GET** method. For example, if a URL might produce a large download, a **HEAD** request could read its _Content-Length_ header to check the filesize without actually downloading the file.

If the response to a **HEAD** request shows that a cached URL response is now outdated, the cached copy is invalidated even if no **GET** request was made.

|                              |    |
|------------------------------|----|
| Request has body             | ❌ |
| Successful response has body | ❌ |
| Safe                         | ✔️ |
| Idempotent                   | ✔️ |
| Cacheable                    | ✔️ |
| Allowed in HTML forms        | ❌ |

## POST

The **HTTP POST** method sends data to the server. The type of the body of the request is indicated by the _Content-Type_ header.

A **POST** request is typically sent via an HTML form and results in a change on the server. In this case, the content type is selected by putting the adequate string in the enctype attribute of the _<form>_ element or the formenctype attribute of the _<input>_ or _<button>_ elements:

- _**application/x-www-form-urlencoded**_: the keys and values are encoded in key-value tuples separated by '&', with a '=' between the key and the value. Non-alphanumeric characters in both keys and values are percent encoded: this is the reason why this type is not suitable to use with binary data (use _multipart/form-data_ instead)
- _**multipart/form-data**_: each value is sent as a block of data ("body part"), with a user agent-defined delimiter ("boundary") separating each part. The keys are given in the _Content-Disposition_ header of each part.
- _**text/plain**_

When the POST request is sent via a method other than an HTML form — like via an XMLHttpRequest — the body can take any type. As described in the HTTP 1.1 specification, **POST** is designed to allow a uniform method to cover the following functions:

- Annotation of existing resources
- Posting a message to a bulletin board, newsgroup, mailing list, or similar group of articles;
- Adding a new user through a signup modal;
- Providing a block of data, such as the result of submitting a form, to a data-handling process;
- Extending a database through an append operation.

|                              |    |
|------------------------------|----|
| Request has body             | ✔️ |
| Successful response has body | ✔️ |
| Safe                         | ❌ |
| Idempotent                   | ❌ |
| Cacheable                    | Only if freshness information is included |
| Allowed in HTML forms        | ✔️ |    

## PUT
    
The **HTTP PUT** request method creates a new resource or replaces a representation of the target resource with the request payload.
    
|                              |    |
|------------------------------|----|
| Request has body             | ✔️ |
| Successful response has body | ✔️/❌ |
| Safe                         | ❌ |
| Idempotent                   | ✔️ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ | 
    
### POST vs PUT

The difference between **POST** and **PUT** is that **PUT** is idempotent: calling it once or several times successively has the same effect (that is no side effect), whereas successive identical **POST** requests may have additional effects, akin to placing an order several times.
    
## DELETE
    
The **HTTP DELETE** request method deletes the specified resource.

|                              |    |
|------------------------------|----|
| Request has body             | ✔️/❌ |
| Successful response has body | ✔️/❌ |
| Safe                         | ❌ |
| Idempotent                   | ✔️ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ |
    
## PATCH
    
The **HTTP PATCH** request method applies partial modifications to a resource.

**PATCH** is somewhat analogous to the "update" concept found in CRUD (in general, HTTP is different than CRUD, and the two should not be confused).

A **PATCH** request is considered a set of instructions on how to modify a resource. Contrast this with **PUT**; which is a complete representation of a resource.

A **PATCH** is not necessarily idempotent, although it can be. Contrast this with **PUT**; which is always idempotent. The word "idempotent" means that any number of repeated, identical requests will leave the resource in the same state. For example if an auto-incrementing counter field is an integral part of the resource, then a **PUT** will naturally overwrite it (since it overwrites everything), but not necessarily so for **PATCH**.

**PATCH** (like **POST**) may have side-effects on other resources.

To find out whether a server supports **PATCH**, a server can advertise its support by adding it to the list in the Allow or Access-Control-Allow-Methods (for CORS) response headers.

Another (implicit) indication that **PATCH** is allowed, is the presence of the _Accept-Patch_ header, which specifies the patch document formats accepted by the server.
    
|                              |    |
|------------------------------|----|
| Request has body             | ✔️ |
| Successful response has body | ✔️ |
| Safe                         | ❌ |
| Idempotent                   | ❌ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ |
    
## OPTIONS
    
The **HTTP OPTIONS** method requests permitted communication options for a given URL or server. A client can specify a URL with this method, or an asterisk (*) to refer to the entire server.
    
|                              |    |
|------------------------------|----|
| Request has body             | ❌ |
| Successful response has body | ✔️ |
| Safe                         | ✔️ |
| Idempotent                   | ✔️ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ |
    
## CONNECT
    
The **HTTP CONNECT** method starts two-way communications with the requested resource. It can be used to open a tunnel.

For example, the **CONNECT** method can be used to access websites that use SSL (HTTPS). The client asks an HTTP Proxy server to tunnel the TCP connection to the desired destination. The server then proceeds to make the connection on behalf of the client. Once the connection has been established by the server, the Proxy server continues to proxy the TCP stream to and from the client.

**CONNECT** is a hop-by-hop method.
    
|                              |    |
|------------------------------|----|
| Request has body             | ❌ |
| Successful response has body | ❌ |
| Safe                         | ❌ |
| Idempotent                   | ❌ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ |
    
## TRACE
    
The **HTTP TRACE** method performs a message loop-back test along the path to the target resource, providing a useful debugging mechanism.

The final recipient of the request should reflect the message received, excluding some fields described below, back to the client as the message body of a 200 (OK) response with a _Content-Type_ of _message/http_. The final recipient is either the origin server or the first server to receive a _Max-Forwards_ value of 0 in the request.
    
|                              |    |
|------------------------------|----|
| Request has body             | ❌ |
| Successful response has body | ❌ |
| Safe                         | ✔️ |
| Idempotent                   | ✔️ |
| Cacheable                    | ❌ |
| Allowed in HTML forms        | ❌ |
    
All information was copied from [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
