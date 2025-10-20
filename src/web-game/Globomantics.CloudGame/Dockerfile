# Use the official .NET 5 SDK image for build stage
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

# copy csproj and restore as distinct layers
COPY ["Globomantics.CloudGame.csproj", "./"]
RUN dotnet restore "Globomantics.CloudGame.csproj"

# copy everything else and build
COPY . .
RUN dotnet publish "Globomantics.CloudGame.csproj" -c Release -o /app/publish

# runtime image
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish ./
EXPOSE 80
ENTRYPOINT ["dotnet", "Globomantics.CloudGame.dll"]
