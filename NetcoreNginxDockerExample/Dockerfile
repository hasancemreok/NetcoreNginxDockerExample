FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /app
ENV CURRENT_DIR="/app"
EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 5001

#COPY ["NetcoreNginxDockerExample.csproj", "NetcoreNginxDockerExample/"]
ADD . .
COPY . .
#RUN dotnet restore "NetcoreNginxDockerExample.csproj"

FROM build AS publish
RUN dotnet publish "${CURRENT_DIR}/NetcoreNginxDockerExample.csproj" -c release -r linux-x64 -o "${CURRENT_DIR}/publish"

WORKDIR /dotnetapp
COPY --from=publish /app/publish/ .

ENTRYPOINT ["dotnet", "NetcoreNginxDockerExample.dll"]