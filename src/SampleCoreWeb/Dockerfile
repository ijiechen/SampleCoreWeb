FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY SampleCoreWeb/*.csproj ./SampleCoreWeb/
RUN dotnet restore

# copy everything else and build app
COPY SampleCoreWeb/. ./SampleCoreWeb/
WORKDIR /app/SampleCoreWeb
RUN dotnet publish -c Release -o out


FROM microsoft/dotnet:2.1-aspnetcore-runtime AS runtime
WORKDIR /app
COPY --from=build /app/SampleCoreWeb/out ./
ENTRYPOINT ["dotnet", "SampleCoreWeb.dll"]