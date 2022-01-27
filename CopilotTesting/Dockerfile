FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CopilotTesting/CopilotTesting.csproj", "CopilotTesting/"]
RUN dotnet restore "CopilotTesting/CopilotTesting.csproj"
COPY . .
WORKDIR "/src/CopilotTesting"
RUN dotnet build "CopilotTesting.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CopilotTesting.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CopilotTesting.dll"]
