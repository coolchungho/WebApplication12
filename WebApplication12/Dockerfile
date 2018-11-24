FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WebApplication12/WebApplication12.csproj", "WebApplication12/"]
RUN dotnet restore "WebApplication12/WebApplication12.csproj"
COPY . .
WORKDIR "/src/WebApplication12"
RUN dotnet build "WebApplication12.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication12.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication12.dll"]