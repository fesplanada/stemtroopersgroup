#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["stemtroopers.client/stemtroopers.client.csproj", "stemtroopers.client/"]
RUN dotnet restore "stemtroopers.client/stemtroopers.client.csproj"
COPY . .
WORKDIR "/src/stemtroopers.client"
RUN dotnet build "stemtroopers.client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "stemtroopers.client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "stemtroopers.client.dll"]