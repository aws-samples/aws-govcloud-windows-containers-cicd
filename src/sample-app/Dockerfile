# === App built on agent ===
#FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019
#ARG source
#WORKDIR /inetpub/wwwroot
#COPY simpleapp/bin/publish/ .

# === App built inside containers ===
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
WORKDIR /app
COPY . .
RUN nuget restore
RUN msbuild .\simpleapp\simpleapp.csproj /p:DeployOnBuild=true /p:PublishProfile=Publish
RUN dir simpleapp/bin
# copy build artifacts into runtime image
FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8-windowsservercore-ltsc2019 AS runtime
WORKDIR /inetpub/wwwroot
COPY --from=build /app/simpleapp/bin/publish/. ./
