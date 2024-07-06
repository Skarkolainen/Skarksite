
# Build image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy root project
COPY ["BlazorWasm.csproj", "./"]
RUN dotnet restore "./BlazorWasm.csproj"

# Copy the rest of src
COPY . .

# Build and publish
RUN dotnet publish "BlazorWasm.csproj" -c Release -o /app/publish

# Serve
FROM nginx:alpine AS final
WORKDIR /usr/share/nginx/html

# Copy the build output to the Nginx html directory
COPY --from=build /app/publish/wwwroot .

# COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]