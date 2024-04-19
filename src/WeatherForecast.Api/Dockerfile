# Estágio 1: Compilação e construção da aplicação
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copiar csproj e restaurar dependências
# Caminho atualizado para o csproj, que está no mesmo diretório que o Dockerfile
COPY WeatherForecast.Api/*.csproj ./WeatherForecast.Api/
RUN dotnet restore WeatherForecast.Api/

# Copiar os arquivos do projeto e construir a aplicação
COPY WeatherForecast.Api/ ./WeatherForecast.Api/
RUN dotnet publish WeatherForecast.Api/ -c Release -o out

# Estágio 2: Configurar a imagem de execução
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .

# Definir a variável de ambiente para habilitar a detecção de Docker no .NET
ENV ASPNETCORE_URLS=http://+:80
EXPOSE 80

ENTRYPOINT ["dotnet", "WeatherForecast.Api.dll"]
