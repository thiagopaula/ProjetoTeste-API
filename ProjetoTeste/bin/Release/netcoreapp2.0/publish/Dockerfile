FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["ProjetoTeste/ProjetoTeste.csproj", "ProjetoTeste/"]
RUN dotnet restore "ProjetoTeste/ProjetoTeste.csproj"
COPY . .
WORKDIR "/src/ProjetoTeste"
RUN dotnet build "ProjetoTeste.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ProjetoTeste.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ProjetoTeste.dll"]

FROM microsoft/aspnetcore
WORKDIR /app
COPY . .
CMD ASPNETCORE_URLS=http://*:$PORT dotnet ProjetoTeste.dll