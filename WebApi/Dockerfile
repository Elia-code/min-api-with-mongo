# Phase 1: Build & Publish
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Kopiere die Projektdatei und restore die Abhängigkeiten
COPY ["WebApi.csproj", "./"]
RUN dotnet restore "WebApi.csproj"

# Kopiere den restlichen Code und veröffentliche die App
COPY . .
RUN dotnet publish "WebApi.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Phase 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .

# Umgebungsvariable setzen, damit die App auf Port 5001 hört
ENV ASPNETCORE_URLS=http://+:5001
EXPOSE 5001

ENTRYPOINT ["dotnet", "WebApi.dll"]