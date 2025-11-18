# Build stage
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /app
COPY --from=build /app/publish .

# This line tells Docker (and ACI) which port the app uses
EXPOSE 80

# This ensures ASP.NET Core listens on port 80, not 5000
ENV ASPNETCORE_URLS=http://+:80

ENTRYPOINT ["dotnet", "BlazorAppDemo.dll"]
