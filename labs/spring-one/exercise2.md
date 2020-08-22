﻿---
uid: labs/spring-one/exercise2
_disableToc: true
---
[vs-run-application]: ~/labs/images/vs-run-application.png "Run the project"
[run-weatherforecast]: ~/labs/images/weatherforecast-endpoint.png "Weatherforecast endpoint"

[home-page-link]: index.md
[exercise-1-link]: exercise1.md
[exercise-2-link]: exercise2.md
[exercise-3-link]: exercise3.md
[exercise-4-link]: exercise4.md

|[Back to intro](index.md)&nbsp;&nbsp;&nbsp;|
|---------:|

# Exploring all actuators

## Goal

See all actuators running and learn what options are available.

## Expected Results

Enhance the app created in the previous exercise to enable all actuator endpoints.

## Get Started

Open `Program.cs` and replace the 3 Steeltoe "Add" statements with the single "all actuators" statement.

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
	Host.CreateDefaultBuilder(args)
		.ConfigureWebHostDefaults(webBuilder => {
			webBuilder.UseStartup<Startup>();
		})

		//Steeltoe actuators
		.AddAllActuators()
		;
```

Expose all the actuator endpoints for debugging and demonstration purpose in `appsettings.json`.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Steeltoe": "Information"
    }
  },
  "AllowedHosts": "*",
  "management": {
    "endpoints": {
      "actuator": {
        "exposure": {
          "include": [ "*" ]
        }
      }
    }
  }
}
```

## Run the application

With all actuators implemented in host builder, start the application by clicking the `Debug > Start Debugging` top menu item.

# [.NET CLI](#tab/dotnet-cli)

```powershell
dotnet run
```

# [Visual Studio](#tab/visual-studio)

![vs-run-application]

***

Once started your default browser should open and automatically load the weather forecast endpoint.

![run-weatherforecast]

## Discover all the management endpoints

What exactly has happened? In the previous exercise 3 of the endpoints where implemented and we visited each in the browser to see their output. There was no need to expose those select endpoints because by default Steeltoe doesn't secure them (you can [if you want](https://steeltoe.io/docs/3/management/using-endpoints#exposing-endpoints)). With the addition of all endpoints, there are some that are secured by default. Here's a list of each endpoint that is available and it's purpose. While the application is running visit each one to learn more.

- `/actuators`: A json structured list of all actuator endpoints that have been exposed.
- `/actuators/env`: A listing of all environment variables that are available to the app.
- `/actuators/health`: The current health status of the app as reported in IHealthContributor, customized for different platforms.
- `/actuators/info`: Various app information collected from the IInfoContributor.
- `/actuators/loggers`: View and configure the logging levels of your application at runtime. This endpoints supports POST requests to adjust logging levels.
- `/actuator/mappings`: Details about automatically discovered MVC and WebAPI project routes and route templates.
- `/actuators/metrics`: App CLR and HTTP metrics collected using OpenTelemetry library.
- `/actuators/prometheus`: A copy of the metrics endpoint, in a Prometheus friendly format.
- `/actuators/refresh`: Trigger the app’s IConfigurationRoot to automatically refresh all configuration values.
- `/actuators/tracing`: Details about the last few request traces made by the app.

## Summary

Similar to the previous exercise, there is a minimum expectation of any microserivce running in the cloud. These things are meant to help the developer debug, trace, and observe the application within its container. But these things have the potential to consume the developer's time creating everything, adding the right options, and making it distributable. Steeltoe aims to use the best in .NET to get the developer back to coding business logic and not deal with the boilerplate stuff.


|[<< Previous Exercise][exercise-1-link]|[Next Exercise >>][exercise-3-link]|
|:--|--:|