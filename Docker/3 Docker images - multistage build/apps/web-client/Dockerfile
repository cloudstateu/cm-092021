FROM mcr.microsoft.com/dotnet/sdk:3.1
COPY . ./web_client
WORKDIR /web_client/
RUN dotnet build -c Release
ENTRYPOINT ["dotnet", "run", "-c", "Release", "--no-build"]
