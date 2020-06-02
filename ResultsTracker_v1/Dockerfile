#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["ResultsTracker_v1/ResultsTracker_v1.csproj", "ResultsTracker_v1/"]
RUN dotnet restore "ResultsTracker_v1/ResultsTracker_v1.csproj"
COPY . .
WORKDIR "/src/ResultsTracker_v1"
RUN dotnet build "ResultsTracker_v1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ResultsTracker_v1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ResultsTracker_v1.dll"]