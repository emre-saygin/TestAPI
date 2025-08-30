# 1. Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# csproj ve restore
COPY ["TestAPI.csproj", "TestAPI/"]
RUN dotnet restore "TestAPI.csproj"

# Tüm proje dosyalarýný kopyala
COPY . .
WORKDIR /src/TestAPI

# Publish (Release)
RUN dotnet publish "TestAPI.csproj" -c Release -o /app/publish

# 2. Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "TestAPI.dll"]