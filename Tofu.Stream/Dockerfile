FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Tofu.Stream/Tofu.Stream.csproj", "Tofu.Stream/"]
RUN dotnet restore "Tofu.Stream/Tofu.Stream.csproj"
COPY . .
WORKDIR "/src/Tofu.Stream"
RUN dotnet build "Tofu.Stream.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Tofu.Stream.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Tofu.Stream.dll"]
