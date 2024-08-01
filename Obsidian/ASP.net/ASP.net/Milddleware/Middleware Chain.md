---
tags:
  - Asp_Net_Core
  - Middleware
---

# Middleware Chain
---

![[4.png]]

![[Milddleware/img/5.png]]

![[Milddleware/img/6.png]]


## `app.Use` in ASP.NET Core

In ASP.NET Core, `app.Use` is a method used to add middleware to the application's request processing pipeline. Middleware added with `app.Use` is not terminal, meaning it does not end the request processing; instead, it can pass the request to subsequent middleware in the pipeline.

### Usage

```CSharp
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Hello\n");
    await next(context);
});
```

#### Explanation

- **Middleware**: Like `app.Run`, `app.Use` adds middleware to the request pipeline. However, `app.Use` does not short-circuit the pipeline; it allows other middleware components to be executed after it.
    
- **RequestDelegate**: This is a delegate that represents the next middleware component in the pipeline. It is used to invoke the next middleware.
    
- **`next(context)`**: Calling `next(context)` passes the request to the next middleware component. This is crucial for ensuring that the request continues through the pipeline.

##### Example Breakdown

1. **Middleware Execution**: The middleware defined in `app.Use` executes first. In this example, it writes "Hello\n" to the response body.
    
2. **Passing to Next Middleware**: After writing to the response, `await next(context)` is called. This invokes the next middleware in the pipeline. If this line is omitted, the request processing will be terminated at this middleware, and no subsequent middleware will be executed.
	```CSharp
	app.Use(async (HttpContext context, RequestDelegate next) =>
	{
	    await context.Response.WriteAsync("Hello\n"); // Executes first
	    await next(context); // Passes the request to the next middleware
	});
	```
	
3. **Subsequent Middleware**: Any middleware added after this `app.Use` call will be executed after this middleware has completed. For example:
	```CSharp
	app.Use(async (HttpContext context, RequestDelegate next) =>
	{
	    await context.Response.WriteAsync("World\n"); // Executes after "Hello\n"
	});
	```

In this case, the final output would be "Hello\nWorld\n", assuming `app.Use` middleware is called before this one in the pipeline.

### Benefits

- **Chaining**: Allows multiple middleware components to be chained together, providing a flexible request processing pipeline.
- **Non-Terminal Processing**: Enables the continuation of request processing through subsequent middleware components.
- **Conditional Execution**: You can conditionally invoke `next` based on certain logic, affecting the flow of request processing.


