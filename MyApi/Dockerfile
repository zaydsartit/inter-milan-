# 1 Build stage: Use .NET SDK image (for building the app)
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# 2 Set working directory inside the container
WORKDIR /src

# 3 Copy .csproj file to container (only csproj)
COPY *.csproj ./

# 4 Restore NuGet dependencies
RUN dotnet restore

# 5 Copy the rest of your code
COPY . ./

# 6 Publish the app (build & prepare for production)
RUN dotnet publish -c Release -o /app/publish

# 7 Runtime stage: use lighter image (only runtime)
FROM mcr.microsoft.com/dotnet/aspnet:8.0

# 8 Set the working directory
WORKDIR /app

# 9 Copy build output from previous stage to runtime image
COPY --from=build /app/publish .

# 10 Expose the port your app runs on (5000)
EXPOSE 5170

# 🚀 Define the command to run your app
ENTRYPOINT ["dotnet", "MyApi.dll"]
