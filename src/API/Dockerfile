FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 52027
EXPOSE 44377

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY src/API/API.csproj src/API/
RUN dotnet restore src/API/API.csproj
COPY . .
WORKDIR /src/src/API
RUN dotnet build API.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish API.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "API.dll"]
