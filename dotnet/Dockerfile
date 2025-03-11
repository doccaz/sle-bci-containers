# Estágio 1: Build application
FROM registry.suse.com/bci/dotnet-sdk:7.0 AS build
WORKDIR /src

#Cria um novo console
RUN dotnet new console -o app-exemplo-dotnet
WORKDIR /src/app-exemplo-dotnet

#Restaura as dependencias
RUN dotnet restore

#Build na aplicação
RUN dotnet publish --configuration Release --output /app/publish


# Estágio 2: Roda a aplicação
FROM registry.suse.com/bci/dotnet-runtime:7.0
WORKDIR /app

# Copia a saída do estágio de build 
COPY --from=build /app/publish .

# Seta o entry point para executar a aplicação
ENTRYPOINT ["dotnet", "app-exemplo-dotnet.dll"]
