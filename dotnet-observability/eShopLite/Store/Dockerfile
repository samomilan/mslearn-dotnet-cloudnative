FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /DataEntities
COPY "eShopLite/DataEntities/DataEntities.csproj" .
RUN dotnet restore
COPY "eShopLite/DataEntities" .
RUN dotnet publish -c release -o /app

WORKDIR /src
COPY "eShopLite" .
RUN dotnet restore Store/Store.csproj
RUN dotnet publish Store/Store.csproj -c release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Store.dll"]