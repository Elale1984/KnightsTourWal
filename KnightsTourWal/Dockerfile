FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["KnightsTourWal/KnightsTourWal.csproj", "KnightsTourWal/"]
RUN dotnet restore "KnightsTourWal/KnightsTourWal.csproj"
COPY . .
WORKDIR "/src/KnightsTourWal"
RUN dotnet build "KnightsTourWal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KnightsTourWal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KnightsTourWal.dll"]
