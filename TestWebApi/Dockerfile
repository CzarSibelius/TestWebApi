#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
#WORKDIR /src
#COPY ["TestWebApi/TestWebApi.csproj", "TestWebApi/"]
#RUN dotnet restore "TestWebApi/TestWebApi.csproj"
#COPY . .
#WORKDIR "/src/TestWebApi"
#RUN dotnet build "TestWebApi.csproj" -c Release -o /app/build
#
#FROM build AS publish
#RUN dotnet publish "TestWebApi.csproj" -c Release -o /app/publish
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "TestWebApi.dll"]

## Builder
#FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
#WORKDIR /app
## Copy csproj and restore as distinct layers
#COPY aspnetcore/src/api/api.csproj ./
#RUN dotnet restore
## Copy everything else and build
#COPY aspnetcore/src/api/ ./
#RUN dotnet publish -c Release -o out
#
#
#
## Runtime image
#FROM mcr.microsoft.com/dotnet/aspnet:5.0
#WORKDIR /app
#COPY --from=build-env /app/out .
#EXPOSE 8080
#ENTRYPOINT ["dotnet", "api.dll"]


# Builder
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app
# Copy csproj and restore as distinct layers
#COPY aspnetcore/src/api/api.csproj ./
COPY ["TestWebApi/TestWebApi.csproj", "TestWebApi/"]
#RUN dotnet restore
RUN dotnet restore "TestWebApi/TestWebApi.csproj"
# Copy everything else and build
#COPY aspnetcore/src/api/ ./
COPY . .
RUN dotnet publish -c Release -o out



# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .
EXPOSE 8080
ENTRYPOINT ["dotnet", "TestWebApi.dll"]