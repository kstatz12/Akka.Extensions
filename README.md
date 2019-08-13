# [Akka.Net](https://getakka.net) integrate with [Microsoft.Extensions](https://github.com/aspnet/Extensions)

[![Build Status](https://iron9light.visualstudio.com/github/_apis/build/status/iron9light.Akka.Extensions?branchName=master)](https://iron9light.visualstudio.com/github/_build/latest?definitionId=4&branchName=master)
[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=iron9light_Akka.Extensions&metric=ncloc)](https://sonarcloud.io/dashboard?id=iron9light_Akka.Extensions)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=iron9light_Akka.Extensions&metric=coverage)](https://sonarcloud.io/dashboard?id=iron9light_Akka.Extensions)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=iron9light_Akka.Extensions&metric=reliability_rating)](https://sonarcloud.io/dashboard?id=iron9light_Akka.Extensions)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=iron9light_Akka.Extensions&metric=security_rating)](https://sonarcloud.io/dashboard?id=iron9light_Akka.Extensions)

## Akka.DI.Extensions.DependencyInjection

[Microsoft.Extensions.DependencyInjection](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection) Dependency Injection (DI) support for [Akka.NET](https://getakka.net/articles/actors/dependency-injection.html)

[![NuGet](https://img.shields.io/nuget/v/Akka.DI.Extensions.DependencyInjection.svg)](https://www.nuget.org/packages/Akka.DI.Extensions.DependencyInjection/)

```csharp
// Create and build your container
var builder = new ServiceCollection();
builder.AddTransient<IWorkerService, IWorkerService>();
builder.AddTransient<TypedWorker>();
var serviceProvider = builder.BuildServiceProvider();

// Create the ActorSystem and Dependency Resolver
var system = ActorSystem.Create("MySystem");
system.UseServiceProvider(serviceProvider);
```

## Akka.Logger.Extensions.Logging

[Microsoft.Extensions.Logging](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging) logging adapter for [Akka.NET](https://getakka.net/articles/utilities/logging.html)

[![NuGet](https://img.shields.io/nuget/v/Akka.Logger.Extensions.Logging.svg)](https://www.nuget.org/packages/Akka.Logger.Extensions.Logging/)

You'll need to set the static property `LoggingLogger.LoggerFactory` and also specify to use the logger in the config when creating the system, for example like this:

```csharp
var builder = new ServiceCollection()
    .AddLogging(logging => logging.AddConsole().AddDebug());
var serviceProvider = builder.BuildServiceProvider();
var loggerFactory = serviceProvider.GetRequiredService<ILoggerFactory>();

LoggingLogger.LoggerFactory = loggerFactory;

var system = ActorSystem.Create("my-test-system", "akka { loglevel=INFO,  loggers=[\"Akka.Logger.Extensions.Logging.LoggingLogger, Akka.Logger.Extensions.Logging\"]}");
```

To log inside an actor:

```csharp
var log = Context.GetLogger();
...
log.Info("The value is {Counter}", counter);
```
