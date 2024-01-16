FROM mcr.microsoft.com/dotnet/nightly/sdk AS build
WORKDIR /app

#copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore 

#copy everything else and build app
COPY . ./
WORKDIR /app
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:7.0 as runtime
WORKDIR /app
COPY --from=build /app/out ./
ENTRYPOINT ["dotnet", "HelloWorldApp.Web.dll"]