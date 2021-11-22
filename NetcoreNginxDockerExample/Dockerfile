FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base

EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 5001

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build

#COPY ["NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
ADD . .
COPY . .
RUN dotnet restore "NetcoreNginxDockerExample.csproj"

FROM build AS publish
RUN dotnet publish "NetcoreNginxDockerExample.csproj" -c release -r linux-x64 -o "/app/publish"

COPY --from=publish /app/publish/ /dotnetapp

FROM base AS final
ENTRYPOINT ["dotnet", "/dotnetapp/NetcoreNginxDockerExample.dll"]