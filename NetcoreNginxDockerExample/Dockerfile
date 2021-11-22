FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 5001

#COPY ["NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
ADD . .
#RUN dotnet restore "NetcoreNginxDockerExample.csproj"

RUN dotnet publish "NetcoreNginxDockerExample.csproj" -c release -r linux-x64 -o "/app/publish"

COPY --from=build /app/publish/ /dotnetapp

FROM base AS final
ENTRYPOINT ["dotnet", "/dotnetapp/NetcoreNginxDockerExample.dll"]