# Use the SDK image for building the app
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY Tailspin.SpaceGame.Web.csproj .
RUN dotnet restore

# Copy everything else and build the project
COPY . .
RUN dotnet build -c Release -o /app/build

# Publish the project
RUN dotnet publish -c Release -o /app/publish

# Use the runtime image for running the app
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Tailspin.SpaceGame.Web.dll"]

