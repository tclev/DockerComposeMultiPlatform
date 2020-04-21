FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR "/src/ApiTier"
COPY . .
RUN dotnet build "WebApi.csproj" -c Debug -o /app

FROM build AS publish
RUN dotnet publish "WebApi.csproj" -c Debug -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApi.dll"]