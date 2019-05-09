FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine3.9 AS build-env
WORKDIR /app

COPY ./src/Core Core
COPY ./src/Dto Dto
COPY ./src/Services Services
COPY ./src/Api Api

RUN dotnet publish ./Api/*.csproj -c Release -o out

FROM mcr.microsoft.com/dotnet/core/runtime:2.2-alpine3.9
        
ENV DBSERVER localhost
ENV DBUSERID sa
ENV DBPASSWORD 123
ENV DBNAME accountgo

EXPOSE 8001

WORKDIR /app

COPY --from=build-env /app/Api/out ./

ENTRYPOINT ["dotnet", "Api.dll"]