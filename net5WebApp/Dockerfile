#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["net5WebApp/net5WebApp.csproj", "net5WebApp/"]
RUN dotnet restore "net5WebApp/net5WebApp.csproj"
COPY . .
WORKDIR "/src/net5WebApp"
RUN dotnet build "net5WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "net5WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "net5WebApp.dll"]