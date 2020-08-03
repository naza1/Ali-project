#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["AliProject/AliProject.csproj", "AliProject/"]
RUN dotnet restore "AliProject/AliProject.csproj"
COPY . .
WORKDIR "/src/AliProject"
RUN dotnet build "AliProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AliProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AliProject.dll"]