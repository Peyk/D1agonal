FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["D1agonal.Pubkey/D1agonal.Pubkey.csproj", "D1agonal.Pubkey/"]
RUN dotnet restore "D1agonal.Pubkey/D1agonal.Pubkey.csproj"
COPY . .
WORKDIR "/src/D1agonal.Pubkey"
RUN dotnet build "D1agonal.Pubkey.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "D1agonal.Pubkey.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "D1agonal.Pubkey.dll"]