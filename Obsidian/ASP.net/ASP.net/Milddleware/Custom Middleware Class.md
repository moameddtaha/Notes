---
tags:
  - Asp_Net_Core
  - Middleware
---

# Custom Middleware Class
---

![[Milddleware/img/7.png]]

![[Milddleware/img/8.png]]

## `builder.Services.AddTransient<MyCustomMiddleware>();` in ASP.NET Core

In ASP.NET Core, dependency injection (DI) is a fundamental concept used to manage dependencies within an application. When you register services with the DI container, you specify how instances of the services are created and their lifetimes.

The line `builder.Services.AddTransient<MyCustomMiddleware>();` is used to register the `MyCustomMiddleware` class with the DI container as a transient service. Here's a detailed explanation:

### Explanation

- **Dependency Injection (DI)**: DI is a design pattern used to implement IoC (Inversion of Control). It allows the creation of dependent objects outside of a class and provides those objects to a class through different ways (constructor, method, or property).
    
- **Service Lifetime**: In ASP.NET Core, services can have different lifetimes:
    
    - ==**Transient**==: A new instance is created each time the service is requested.
    - ==**Scoped**==: A new instance is created once per request.
    - ==**Singleton**==: A single instance is created and shared throughout the application's lifetime.
	
- **AddTransient**: When you use `AddTransient`, you're specifying that a new instance of the `MyCustomMiddleware` class should be created every time it is requested from the DI container.

```CSharp
builder.Services.AddTransient<MyCustomMiddleware>();
```

- **Service Registration**: This line registers the `MyCustomMiddleware` class as a transient service. It means that every time `MyCustomMiddleware` is needed (for example, when the `UseMiddleware<MyCustomMiddleware>()` is called), a new instance will be created.

#### Usage in Middleware

1. **Middleware Registration**: By registering `MyCustomMiddleware` with `AddTransient`, you make it available to be used in the middleware pipeline.
    
2. **Middleware Execution**: When `app.UseMiddleware<MyCustomMiddleware>()` is called, the DI container resolves `MyCustomMiddleware` and injects it into the middleware pipeline. Since `AddTransient` is used, a new instance of `MyCustomMiddleware` is created for each request.

##### Example Middleware Pipeline

```CSharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddTransient<MyCustomMiddleware>();
var app = builder.Build();

// Middleware 1
app.Use(async (HttpContext context, RequestDelegate next) =>
{
    await context.Response.WriteAsync("Middleware 1- Starts\n");
    await next(context);
    await context.Response.WriteAsync("Middleware 1- Ends\n");
});

// Middleware 2
app.UseMiddleware<MyCustomMiddleware>();

// Middleware 3
app.Run(async (HttpContext context) =>
{
    await context.Response.WriteAsync("Middleware 3.\n");
});

app.Run();
```

###### Breakdown

- **Middleware 1**: An inline delegate middleware that writes "Middleware 1- Starts" and "Middleware 1- Ends" around the execution of the next middleware.
- **Middleware 2**: The `MyCustomMiddleware` class registered as transient is invoked here. Each request gets a new instance of `MyCustomMiddleware`.
- **Middleware 3**: The terminal middleware that writes "Middleware 3." and stops further processing of the request.

