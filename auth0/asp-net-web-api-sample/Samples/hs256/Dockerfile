#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 3010

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["HS256.csproj", ""]
RUN dotnet restore "./HS256.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "HS256.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HS256.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HS256.dll"]