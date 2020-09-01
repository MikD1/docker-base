FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app
COPY . ./
RUN dotnet restore

WORKDIR /app/Tests
RUN dotnet test --logger:trx

WORKDIR /app/Service
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
COPY --from=build /app/Service/out .
ENTRYPOINT ["dotnet", "Service.dll"]