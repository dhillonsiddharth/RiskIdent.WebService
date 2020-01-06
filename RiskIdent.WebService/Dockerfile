FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["RiskIdent.WebService/RiskIdent.WebService.csproj", "RiskIdent.WebService/"]

RUN dotnet restore "RiskIdent.WebService/RiskIdent.WebService.csproj"
COPY . .
WORKDIR "/src/RiskIdent.WebService"
RUN dotnet build "RiskIdent.WebService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RiskIdent.WebService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RiskIdent.WebService.dll"]