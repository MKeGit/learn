The purpose of a web application is to receive and respond to HTTP requests. A request is received, and then the server generates the appropriate response. Everything in ASP.NET Core is concerned with this request/response cycle.

When an ASP.NET Core app receives an HTTP request, it passes through a series of components to generate the response. These components are called middleware. Middleware can be thought of as a pipeline that the request flows through, and each middleware layer can run code before and after the next layer in the pipeline.

:::image type="content" source="../media/request-delegate-pipeline.png" alt-text="A diagram depicting an HTTP request as it's multiple middleware." lightbox="../media/request-delegate-pipeline.png":::

## Middleware and delegates

Middleware is implemented as a delegate that takes a `HttpContext` object and returns a `Task`. The `HttpContext` object represents the current request and response. The delegate is a function that processes the request and response.

For example, consider the following code:

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello world!");
});

app.Run();
```

In the preceding code:

- `WebApplication.CreateBuilder(args)` creates a new `WebApplicationBuilder` object.
- `builder.Build()` creates a new `WebApplication` object.
- The first `app.Run()` defines a delegate that takes a `HttpContext` object and returns a `Task`. The delegate writes "Hello world!" to the response.
- The second `app.Run()` starts the app.

When the app receives an HTTP request, the delegate is called. The delegate writes "Hello world!" to the response and completes the request.

## Chaining middleware

In most apps, you have multiple middleware components that run in sequence. The order in which you add middleware components to the pipeline is important. The components run in the order they were added.

### Terminal and nonterminal middleware

Each middleware can be thought of as terminal or nonterminal. Nonterminal middleware processes the request and then calls the next middleware in the pipeline. Terminal middleware is the last middleware in the pipeline and doesn't have a next middleware to call.

Delegates added with `app.Use()` can be terminal or nonterminal middleware. These delegates expect a `HttpContext` object and a `RequestDelegate` object as parameters. Typically the delegate is

Delegates added with `app.Run()` are *always* terminal middleware. They don't call the next middleware in the pipeline. They're the last middleware component that runs. They only expect a `HttpContext` object as a parameter. `app.Run()` is a shortcut for adding terminal middleware.

Consider the following example:

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.Use(async (context, next) =>
{
    await context.Response.WriteAsync("Hello from middleware 1. Passing to the next middleware!\r\n");

    // Call the next middleware in the pipeline
    await next.Invoke();

    await context.Response.WriteAsync("Hello from middleware 1 again!\r\n");
});

app.Run(async context =>
{
    await context.Response.WriteAsync("Hello from middleware 2!\r\n");
});

app.Run();
```

In the preceding code:

- `app.Use()` defines a middleware component that:
    - Writes "Hello from middleware 1. Passing to the next middleware!" to the response.
    - Passes the request to the next middleware component in the pipeline and waits for it to complete with `await next.Invoke()`.
    - After the next component in the pipeline completes, it writes "Hello from middleware 1 again!"
- The first `app.Run()` defines a middleware component that writes "Hello from middleware 2!" to the response.
- The second `app.Run()` starts the app.

At runtime, when a web browser sends a request to this app, the middleware components run in the order they were added to the pipeline. The app returns the following response:

```output
Hello from middleware 1. Passing to the next middleware!
Hello from middleware 2!
Hello from middleware 1 again!
```

## Built-in middleware

ASP.NET Core provides a set of built-in middleware components that you can use to add common functionality to your app. In addition to the explicitly added middleware components, some middleware is implicitly added for you by default. For example, `WebApplication.CreateBuilder()` returns a `WebApplicationBuilder` that adds the developer exception page routing middleware, conditionally adds the authentication and authorization middleware if the related services are configured, and adds the endpoint routing middleware.

For example, consider the following *Program.cs* file:

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorComponents()
    .AddInteractiveServerComponents();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error", createScopeForErrors: true);
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();

app.UseAntiforgery();

app.MapStaticAssets();
app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode();

app.Run();
```
In the preceding code:

- `app.UseExceptionHandler()` adds a middleware component that catches exceptions and returns an error page.
- `app.UseHsts()` adds a middleware component that sets the Strict-Transport-Security header.
- `app.UseHttpsRedirection()` adds a middleware component that redirects HTTP requests to HTTPS.
- `app.UseAntiforgery()` adds a middleware component that prevents cross-site request forgery (CSRF) attacks.
- `app.MapStaticAssets()` and `app.MapRazorComponents<App>()` map routes to endpoints, which are then handled by the endpoint routing middleware. The endpoint routing middleware is implicitly added by the `WebApplicationBuilder`.

There are many more built-in middleware components that you can use in your app depending on the type of app and your needs. [Check the documentation for the complete list](/aspnet/core/fundamentals/middleware/?view=aspnetcore-8.0&preserve-view=true).

> [!TIP]
> In this context, methods that start with `Use` are generally for mapping middleware. Methods that start with `Map` are generally for mapping endpoints.

> [!IMPORTANT]
> The order middleware components are added to the pipeline matters! Certain middleware components must run before others to work correctly. Check the documentation for each middleware component to determine the correct order.
