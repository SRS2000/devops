#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY [".", "JenkinsWebApp/"]
RUN dotnet restore "JenkinsWebApp/JenkinsWebApp.csproj"
COPY . .
WORKDIR "/src/JenkinsWebApp"
RUN dotnet build "JenkinsWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JenkinsWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsWebApp.dll"]