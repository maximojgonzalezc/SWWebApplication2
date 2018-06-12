FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 60644
EXPOSE 44323

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY SWWebApplication2/SWWebApplication2.csproj SWWebApplication2/
RUN dotnet restore SWWebApplication2/SWWebApplication2.csproj
COPY . .
WORKDIR /src/SWWebApplication2
RUN dotnet build SWWebApplication2.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SWWebApplication2.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SWWebApplication2.dll"]
