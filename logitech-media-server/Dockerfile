FROM debian:bookworm

ARG buildno

# -----------------------------------setup environment
ENV DEBIAN_FRONTEND noninteractive
ENV SQUEEZE_VOL /srv/squeezebox
ENV LANG C.UTF-8
#ENV DEBIAN_FRONTEND noninteractive
ENV PACKAGE_VERSION_URL=https://downloads.lms-community.org/LyrionMusicServer_v9.0.1/lyrionmusicserver_9.0.1_amd64.deb
# ENV PACKAGE_VERSION_URL=https://downloads.lms-community.org/LogitechMediaServer_v8.5.2/logitechmediaserver_8.5.2_amd64.deb
# ENV PACKAGE_VERSION_URL=http://www.mysqueezebox.com/update/?version=8.4.0&revision=1&geturl=1&os=deb
# ENV PACKAGE_VERSION_URL=http://www.mysqueezebox.com/update/?version=8.3.0&revision=1&geturl=1&os=deb
# ENV PACKAGE_VERSION_URL=http://www.mysqueezebox.com/update/?version=8.1.0&revision=1&geturl=1&os=deb
# ENV PACKAGE_VERSION_URL=http://www.mysqueezebox.com/update/?version=7.9.2&revision=1&geturl=1&os=deb
# ENV PACKAGE_VERSION_URL=http://downloads.slimdevices.com/LogitechMediaServer_v7.9.2/logitechmediaserver_7.9.2_amd64.deb

RUN echo "Build number: $buildno"

# RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
RUN     apt-get -qq update && \
	apt-get -yq install \
        apt-utils \           
        && \
        apt-get clean 

# RUN DEBIAN_FRONTEND=noninteractive apt-get -yq install \
RUN apt-get -qq update && \
       apt-get -qq install perl \
       curl \
       wget \
       faad \
       flac \
       lame \
       sox \
       ffmpeg \
       wavpack \
       espeak \
       libcrypt-openssl-rsa-perl libio-socket-inet6-perl libwww-perl \
       libio-socket-ssl-perl \
       tzdata \
       libio-socket-ssl-perl \
       libnet-ssleay-perl \ 
       && \
       apt-get clean

# Download, install, and clean up the package
RUN curl -Lsf -o /tmp/logitechmediaserver.deb "$PACKAGE_VERSION_URL" && \
     dpkg -i /tmp/logitechmediaserver.deb && \
     rm -f /tmp/logitechmediaserver.deb && \
     apt-get clean

#RUN url=$(curl "$PACKAGE_VERSION_URL" | sed 's/_all\.deb/_amd64\.deb/') && \
#	curl -Lsf -o /tmp/logitechmediaserver.deb $url && \
#	dpkg -i /tmp/logitechmediaserver.deb && \
#	rm -f /tmp/logitechmediaserver.deb && \
#	apt-get clean

# This will be created by the entrypoint script.
RUN userdel squeezeboxserver

VOLUME $SQUEEZE_VOL
EXPOSE 3483 3483/udp 9000 9090

COPY include_files/entrypoint.sh /entrypoint.sh
COPY include_files/start-squeezebox.sh /start-squeezebox.sh
RUN chmod 755 /entrypoint.sh /start-squeezebox.sh
ENTRYPOINT ["/entrypoint.sh"]
