FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["supabase-test/supabase-test.csproj", "supabase-test/"]
RUN dotnet restore "supabase-test/supabase-test.csproj"
COPY . .
WORKDIR "/src/supabase-test"
RUN dotnet build "supabase-test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "supabase-test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "supabase-test.dll"]
