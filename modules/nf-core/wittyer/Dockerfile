FROM mcr.microsoft.com/dotnet/sdk:8.0@sha256:8c6beed050a602970c3d275756ed3c19065e42ce6ca0809f5a6fcbf5d36fd305 as builder
WORKDIR /src
COPY . /src
RUN cd Wittyer \
    && dotnet publish -f net6.0 -r linux-x64 -c Release -o /output \
    && chmod +x /output/Wittyer

FROM mcr.microsoft.com/dotnet/runtime:8.0@sha256:39b7ffd4f2fe8522aeef9fa57705ffc6a8123a857458e25403e2c8e39dd40167
LABEL git_repository=https://git.illumina.com/DASTE/Ilmn.Das.App.Wittyer.git
WORKDIR /opt/Wittyer
RUN apt-get -y update && apt-get -y install tabix libunwind8 openssl procps
COPY --from=builder /output /opt/Wittyer
