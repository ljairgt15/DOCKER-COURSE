# Establecer la imagen base para el runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Establecer la imagen base para el SDK
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["PRODUCTSAPI.csproj", "."]
RUN dotnet restore "PRODUCTSAPI.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "PRODUCTSAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PRODUCTSAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PRODUCTSAPI.dll"]
