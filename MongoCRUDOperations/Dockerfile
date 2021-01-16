FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MongoCRUDOperations/MongoCRUDOperations.csproj", "MongoCRUDOperations/"]
RUN dotnet restore "MongoCRUDOperations/MongoCRUDOperations.csproj"
COPY . .
WORKDIR "/src/MongoCRUDOperations"
RUN dotnet build "MongoCRUDOperations.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MongoCRUDOperations.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MongoCRUDOperations.dll"]