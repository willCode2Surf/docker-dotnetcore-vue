FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 3204
EXPOSE 44308

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/MVC/MVC.csproj", "src/MVC/"]
RUN dotnet restore "src/MVC/MVC.csproj"
COPY . .
WORKDIR "/src/src/MVC"
RUN dotnet build "MVC.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MVC.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MVC.dll"]