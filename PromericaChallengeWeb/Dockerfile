# Utiliza la imagen oficial de ASP.NET 7.0
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Utiliza la imagen oficial de SDK para compilar la aplicación
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["PromericaChallenge/PromericaChallengeWeb.csproj", "PromericaChallengeWeb"]
RUN dotnet restore "PromericaChallenge/PromericaChallengeWeb.csproj"
COPY . .
WORKDIR "/src/PromericaChallengeWeb"
RUN dotnet build "PromericaChallengeWeb.csproj" -c Release -o /app/build

# Publica la aplicación
FROM build AS publish
RUN dotnet publish "PromericaChallengeWeb.csproj" -c Release -o /app/publish

# Configura el contenedor final
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PromericaChallengeWeb.dll"]
