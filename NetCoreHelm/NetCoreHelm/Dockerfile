FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["NetCoreHelm.csproj", "NetCoreHelm/"]

#RUN dotnet restore "NetCoreHelm/NetCoreHelm.csproj"
COPY . /src/NetCoreHelm
WORKDIR "/src/NetCoreHelm"
RUN dotnet build "NetCoreHelm.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreHelm.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreHelm.dll"]