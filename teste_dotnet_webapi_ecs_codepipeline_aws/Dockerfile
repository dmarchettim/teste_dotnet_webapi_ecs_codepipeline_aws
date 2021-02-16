#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["teste_dotnet_webapi_ecs_codepipeline_aws/teste_dotnet_webapi_ecs_codepipeline_aws.csproj", "teste_dotnet_webapi_ecs_codepipeline_aws/"]
RUN dotnet restore "teste_dotnet_webapi_ecs_codepipeline_aws/teste_dotnet_webapi_ecs_codepipeline_aws.csproj"
COPY . .
WORKDIR "/src/teste_dotnet_webapi_ecs_codepipeline_aws"
RUN dotnet build "teste_dotnet_webapi_ecs_codepipeline_aws.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "teste_dotnet_webapi_ecs_codepipeline_aws.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "teste_dotnet_webapi_ecs_codepipeline_aws.dll"]