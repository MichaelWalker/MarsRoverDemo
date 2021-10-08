FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MarsRoverDemo/MarsRoverDemo.csproj", "MarsRoverDemo/"]
RUN dotnet restore "MarsRoverDemo/MarsRoverDemo.csproj"
COPY . .
WORKDIR "/src/MarsRoverDemo"
RUN dotnet build "MarsRoverDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MarsRoverDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MarsRoverDemo.dll"]
