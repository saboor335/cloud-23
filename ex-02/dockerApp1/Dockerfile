#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dockerApp1.csproj", "."]
RUN dotnet restore "./dockerApp1.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dockerApp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockerApp1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockerApp1.dll"]