#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["paulorogerio-net.API/paulorogerio-net.API.csproj", "paulorogerio-net.API/"]
RUN dotnet restore "paulorogerio-net.API/paulorogerio-net.API.csproj"
COPY . .
WORKDIR "/src/paulorogerio-net.API"
RUN dotnet build "paulorogerio-net.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "paulorogerio-net.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "paulorogerio-net.API.dll"]