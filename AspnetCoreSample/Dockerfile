FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 21622
EXPOSE 44372

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AspnetCoreSample/AspnetCoreSample.csproj", "AspnetCoreSample/"]
RUN dotnet restore "AspnetCoreSample/AspnetCoreSample.csproj"
COPY . .
WORKDIR "/src/AspnetCoreSample"
RUN dotnet build "AspnetCoreSample.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspnetCoreSample.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspnetCoreSample.dll"]