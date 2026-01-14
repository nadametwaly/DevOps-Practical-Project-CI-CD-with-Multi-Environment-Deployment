FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy solution and project files
COPY *.sln* ./
COPY DotNet-Backend/*.csproj ./DotNet-Backend/
RUN dotnet restore ./DotNet-Backend/

# Copy everything else and build
COPY . .
WORKDIR /src/DotNet-Backend
RUN dotnet publish API.csproj -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "API.dll"]