---
tags:
  - Asp_Net_Core
  - Middleware
---

# `app.Run` in ASP.NET Core

![[3.png]]

In ASP.NET Core, `app.Run` is a method used to add a terminal middleware to the application's request processing pipeline. The term "terminal middleware" means that this middleware is the last one that will handle the request. If you use `app.Run`, no further middleware will be executed after this one.

## Usage

```CSharp
app.Run(async (HttpContext context) =>
{
    // Middleware logic here
});
```

### Explanation

- **Middleware**: A piece of code that sits in the request processing pipeline. Each middleware component can handle the request, modify it, pass it along to the next middleware, or short-circuit the pipeline and generate a response directly. `app.Run` is used to define such middleware.
    
- **Terminal Middleware**: Middleware added with `app.Run` is terminal, meaning it does not call `next()` to pass the request to the next component in the pipeline. Once this middleware is executed, it completes the request processing.
    
- **HttpContext**: An instance of `HttpContext` represents the context of a single HTTP request. It contains information about the request and response, such as request headers, request body, response headers, and methods to interact with the HTTP pipeline.
    
    - **Request**: Provides access to details of the incoming HTTP request (e.g., headers, query string, route data).
    - **Response**: Allows you to configure and send the response back to the client (e.g., status code, headers, response body).

#### Example

In the following example, the `HttpContext` is used to set a simple "Hello, World!" response:

```CSharp
app.Run(async (HttpContext context) =>
{
    await context.Response.WriteAsync("Hello, World!");
});
```

Here, the `HttpContext.Response.WriteAsync` method writes "Hello, World!" to the response body. Since this is terminal middleware, no other middleware will process the request after this one.


