---
layout: post
title: Docker Cheatsheet
author: @craigsaboe
published: 2022-05-24 10:50:00
---

# Commands

## Build

- Build from dockerfile, specifying an identifier.
- Must run from directory containing the dockerfile.

```
docker build --tag something .
```

# Run
- latest is the default version description

```
docker run something:latest
```

# Images
- Reference to check the image's name post-build if needed

```
docker image ls
```

# Dockerfiles

- Basic version (think this is what VS will generate by default)

```
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Something.csproj", "./"]
RUN dotnet restore "Something.csproj"
COPY . ./
RUN dotnet build "Something.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Something.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Something.dll"]
```