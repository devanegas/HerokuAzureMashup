FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["HerokuTest.csproj", "HerokuTest/"]
RUN dotnet restore "HerokuTest/HerokuTest.csproj"
COPY . "./HerokuTest"
WORKDIR "/src/HerokuTest"
RUN dotnet build "HerokuTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HerokuTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
CMD dotnet HerokuTest.dll