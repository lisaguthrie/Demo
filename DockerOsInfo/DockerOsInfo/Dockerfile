FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY DockerOsInfo/DockerOsInfo.csproj DockerOsInfo/
RUN dotnet restore DockerOsInfo/DockerOsInfo.csproj
COPY . .
WORKDIR /src/DockerOsInfo
RUN dotnet build DockerOsInfo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerOsInfo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerOsInfo.dll"]
