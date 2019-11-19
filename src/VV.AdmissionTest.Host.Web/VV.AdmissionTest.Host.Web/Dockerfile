FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web.csproj", "src/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web/"]
RUN dotnet restore "src/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web.csproj"
COPY . .
WORKDIR "/src/src/VV.AdmissionTest.Host.Web/VV.AdmissionTest.Host.Web"
RUN dotnet build "VV.AdmissionTest.Host.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VV.AdmissionTest.Host.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VV.AdmissionTest.Host.Web.dll"]