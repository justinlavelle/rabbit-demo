FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ConsoleAppOne/ConsoleAppOne.csproj ConsoleAppOne/
RUN dotnet restore ConsoleAppOne/ConsoleAppOne.csproj
COPY . .
WORKDIR /src/ConsoleAppOne
RUN dotnet build ConsoleAppOne.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ConsoleAppOne.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ConsoleAppOne.dll"]
