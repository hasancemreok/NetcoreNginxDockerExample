FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
#COPY ["NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
COPY . .
RUN dotnet restore "NetcoreNginxDockerExample/NetcoreNginxDockerExample.csproj"

FROM build AS publish
RUN dotnet publish -c release -r linux-x64 -o "/app/publish" "/src/NetcoreNginxDockerExample/NetcoreNginxDockerExample.csproj"

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NetcoreNginxDockerExample.dll"]