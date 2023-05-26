FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Example.Website.Product.API/Example.Website.Product.API.csproj", "Example.Website.Product.API/"]
RUN dotnet restore "Example.Website.Product.API/Example.Website.Product.API.csproj"
COPY . .
WORKDIR "/src/Example.Website.Product.API"
RUN dotnet build "Example.Website.Product.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Example.Website.Product.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Example.Website.Product.API.dll"]
