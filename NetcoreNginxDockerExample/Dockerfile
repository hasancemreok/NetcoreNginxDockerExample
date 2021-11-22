FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["NetcoreNginxDockerExample/NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
RUN dotnet restore "NetcoreNginxDockerExample/NetcoreNginxDockerExample.csproj"
COPY . .
WORKDIR "/src/NetcoreNginxDockerExample"
RUN dotnet build "NetcoreNginxDockerExample.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NetcoreNginxDockerExample.csproj" -c Release -o /app/publish

FROM base AS final
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NetcoreNginxDockerExample.dll"]