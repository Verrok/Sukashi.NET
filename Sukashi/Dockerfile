FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Sukashi/Sukashi.csproj", "Sukashi/"]
RUN dotnet restore "Sukashi/Sukashi.csproj"
COPY . .
WORKDIR "/src/Sukashi"
RUN dotnet build "Sukashi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Sukashi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Sukashi.dll"]
