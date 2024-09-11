# Start with the .NET 8 SDK image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the remaining source code
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Set the working directory
WORKDIR /app

# Copy the published output from the build stage
COPY --from=build /app/out ./

ENV ASPNETCORE_HTTP_PORTS=80

# Set the entry point
ENTRYPOINT ["dotnet", "RazorPagesTestSample.dll"]