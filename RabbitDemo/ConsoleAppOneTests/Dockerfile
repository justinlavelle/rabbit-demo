FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ConsoleAppOneTests/ConsoleAppOneTests.csproj ConsoleAppOneTests/
COPY ConsoleAppOne/ConsoleAppOne.csproj ConsoleAppOne/
RUN dotnet restore ConsoleAppOneTests/ConsoleAppOneTests.csproj
COPY . .
WORKDIR /src/ConsoleAppOneTests
RUN dotnet build ConsoleAppOneTests.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ConsoleAppOneTests.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ConsoleAppOneTests.dll"]
