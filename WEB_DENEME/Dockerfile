# Temel imaj olarak .NET 7.0 kullan
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

# Uygulama imajını derle
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["HuaweiApiDemo/HuaweiApiDemo.csproj", "HuaweiApiDemo/"]
RUN dotnet restore "HuaweiApiDemo/HuaweiApiDemo.csproj"
COPY . . 
WORKDIR "/src/HuaweiApiDemo"
RUN dotnet build "HuaweiApiDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HuaweiApiDemo.csproj" -c Release -o /app/publish

# Son imajı çalıştır
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HuaweiApiDemo.dll"]
