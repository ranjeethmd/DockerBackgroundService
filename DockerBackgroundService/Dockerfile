FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env


LABEL org.opencontainers.image.title="Docker Worker Services" \
      org.opencontainers.image.description="Dockerized worker services running background work on the servers like data pipeline code etc" \
      org.opencontainers.image.authors="Ranjeeth Malachira Devaiah"


WORKDIR /app

#Copy project file first
COPY *.csproj ./
# Get all the refrences from nuget sources
RUN dotnet restore


#Copy all the other content like source code and config files to /app folder
COPY . ./
RUN dotnet publish -c Release -o out


#Create the run time layer
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app

#Copy and discard the only image for build
COPY --from=build-env /app/out .

# add non root user
RUN useradd -ms /bin/bash app_user


#Add read permission for the user
RUN chown -R app_user /app

#Add the read permission on the folder.
RUN chmod 755 /app

USER app_user


ENTRYPOINT ["dotnet", "DockerBackgroundService.dll"]