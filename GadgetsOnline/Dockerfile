#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS builder

WORKDIR C:\\src
COPY GadgetsOnline.sln .
COPY GadgetsOnline\\GadgetsOnline.csproj GadgetsOnline\\GadgetsOnline.csproj
COPY GadgetsOnline\\Web.config GadgetsOnline\\Web.config
COPY GadgetsOnline\\packages.config GadgetsOnline\\packages.config

RUN nuget restore GadgetsOnline.sln

COPY . C:\\src
RUN msbuild GadgetsOnline\\GadgetsOnline.csproj /p:OutputPath=c:\out /p:Configuration=Release


FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop';"]

ENV APP_ROOT=C:\\inetpub\\wwwroot

WORKDIR ${APP_ROOT}

COPY --from=builder C:\\out\\_PublishedWebsites\\GadgetsOnline ${APP_ROOT}