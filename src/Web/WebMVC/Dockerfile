FROM microsoft/aspnetcore:2.0.3 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore -nowarn:msb3202,nu1503
WORKDIR /src/src/Web/WebMVC
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN bower install --allow-root
RUN dotnet bundle
RUN dotnet publish --no-restore -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebMVC.dll"]
