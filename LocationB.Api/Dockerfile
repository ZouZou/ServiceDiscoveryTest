#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LocationB.Api/LocationB.Api.csproj", "LocationB.Api/"]
RUN dotnet restore "LocationB.Api/LocationB.Api.csproj"
COPY . .
WORKDIR "/src/LocationB.Api"
RUN dotnet build "LocationB.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LocationB.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LocationB.Api.dll"]