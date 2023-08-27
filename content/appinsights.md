Title: Setting up Azure AppInsights
Date: 2022-05-25 11:50:00

# Config
- Create Resource
- Get Connection string
- Add conn string to appsettings.json
```
  "ApplicationInsights": {
    "ConnectionString" : "Copy connection string from Application Insights Resource Overview"
  },
```

# OpenTelemetry
- New spec that's "vendor neutral", MS is going to push that as internals for AppInsight integration

## Setup
```
dotnet add package Azure.Monitor.OpenTelemetry.Exporter --prerelease
dotnet add package OpenTelemetry.Instrumentation.AspNetCore --prerelease
dotnet add package OpenTelemetry.Extensions.Hosting --prerelease
```