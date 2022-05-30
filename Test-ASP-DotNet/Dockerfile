#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Test-ASP-DotNet/Test-ASP-DotNet.csproj", "Test-ASP-DotNet/"]
RUN dotnet restore "Test-ASP-DotNet/Test-ASP-DotNet.csproj"
COPY . .
WORKDIR "/src/Test-ASP-DotNet"
RUN dotnet build "Test-ASP-DotNet.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Test-ASP-DotNet.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Test-ASP-DotNet.dll"]