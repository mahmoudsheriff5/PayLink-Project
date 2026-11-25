FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["PayLinkApi/PayLinkApi.csproj", "PayLinkApi/"]
RUN dotnet restore "PayLinkApi/PayLinkApi.csproj"
COPY . .
RUN dotnet publish "PayLinkApi/PayLinkApi.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
EXPOSE 8080
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "PayLinkApi.dll"]
