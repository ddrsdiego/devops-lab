FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/DevOpsLab.Api/DevOpsLab.Api.csproj", "src/DevOpsLab.Api/"]
RUN dotnet restore "src/DevOpsLab.Api/DevOpsLab.Api.csproj"
COPY . .
WORKDIR "/src/src/DevOpsLab.Api"
RUN dotnet build "DevOpsLab.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevOpsLab.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevOpsLab.Api.dll"]
