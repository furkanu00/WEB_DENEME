# Temel imaj olarak .NET 7.0 kullan
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

# Uygulama imajını derle
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WEB_DENEME/WEB_DENEME.csproj", "WEB_DENEME/"]
RUN dotnet restore "WEB_DENEME/WEB_DENEME.csproj"
COPY . . 
WORKDIR "/src/WEB_DENEME"
RUN dotnet build "WEB_DENEME.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WEB_DENEME.csproj" -c Release -o /app/publish

# Son imajı çalıştır
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WEB_DENEME.dll"]
