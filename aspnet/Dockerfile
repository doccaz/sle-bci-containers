FROM registry.suse.com/bci/dotnet-sdk:9.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY aspnetapp/*.csproj .
RUN dotnet restore

# copy and publish app and libraries
COPY aspnetapp/. .
RUN dotnet publish --no-restore -o /app

# final image
FROM registry.suse.com/bci/dotnet-aspnet:9.0

WORKDIR /app
COPY --from=build /app .

EXPOSE 8080

# uncomment to run as non-root user
# USER $APP_UID

ENTRYPOINT ["./aspnetapp"]

