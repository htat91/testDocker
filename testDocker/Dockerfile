# Sử dụng image .NET 8.0 SDK làm base image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Sao chép file .csproj và restore các dependencies
COPY *.csproj ./
RUN dotnet restore

# Sao chép toàn bộ project và build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .

EXPOSE 44333

ENTRYPOINT ["dotnet", "testDocker.dll"]