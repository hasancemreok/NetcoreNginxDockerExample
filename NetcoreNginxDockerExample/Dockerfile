FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /app
ENV CURRENT_DIR="/app"

#COPY ["NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
ADD . .
COPY . .
#RUN dotnet restore "NetcoreNginxDockerExample.csproj"

RUN dotnet publish "${CURRENT_DIR}/NetcoreNginxDockerExample.csproj" -c release -r linux-x64 -o "${CURRENT_DIR}/publish"

FROM mcr.microsoft.com/dotnet/aspnet:3.1
COPY --from=build /app/publish/ .

RUN apt-get update && apt-get install -y nginx && rm -rf /var/lib/apt/lists/*
COPY --from=build /app/nginx.conf /etc/nginx/

COPY "docker.startup.sh" .
RUN chmod 755 docker.startup.sh
 
ENV ASPNETCORE_URLS http://+:5000
EXPOSE 9090 5001 80

ENTRYPOINT ["sh", "docker.startup.sh"]