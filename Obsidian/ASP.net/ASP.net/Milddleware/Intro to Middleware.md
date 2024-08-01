---
tags:
  - Asp_Net_Core
  - Middleware
---


> [!NOTE] **Middleware**
> Middleware is a sequence of components that execute one after another, each performing specific operations on HTTP requests and responses in a web application.

![[1.png]]

![[2.png]]


# What is Middleware?

- **Definition**: Middleware is a piece of software that acts as a bridge or intermediary between a web server and web applications. It processes HTTP requests and responses in a sequence, allowing you to execute code, modify requests and responses, and handle errors.

## Characteristics of Middleware

1. **Pipeline Execution**:
    
    - Middleware components are executed in a specific order. Each piece of middleware in the pipeline can perform actions before passing the request to the next middleware.
2. **Chain of Responsibility**:
    
    - The sequence of middleware components forms a chain or pipeline. Each component typically has the opportunity to process or modify the request and response.
3. **Request and Response Handling**:
    
    - Middleware can inspect and modify the request before it reaches the final request handler or controller.
    - Similarly, it can modify the response before it is sent back to the client.
4. **Common Uses**:
    
    - **Authentication**: Verify if the user is authenticated.
    - **Logging**: Log details about the request and response.
    - **Error Handling**: Catch and handle exceptions that occur during request processing.
    - **Compression**: Compress the response to reduce payload size.
    - **CORS**: Handle Cross-Origin Resource Sharing settings.


### Middleware Components

- **Definition**: Middleware components are pieces of code that handle HTTP requests and responses. Each component can perform various tasks, such as logging, authentication, or request processing.
- **Characteristics**:
    - Middleware components are typically implemented as classes or a `RequestDelegate`.
    - They are added to the middleware pipeline and execute in a specific order.
    - Each component can perform operations on the request and response, and then either handle the request/response or pass it to the next component in the pipeline.

### Middleware Methods

- **Definition**: Middleware methods are specific functions or methods within a middleware component that perform the actual work.
- **Characteristics**:
    - Middleware methods are often defined in a class or function that implements the `Invoke` or `InvokeAsync` method.
    - These methods contain the logic to process requests and responses.
    - In ASP.NET Core, middleware methods are invoked by the framework as part of the request processing pipeline.



