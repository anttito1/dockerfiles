FROM debian:bullseye-20201209-slim

ENV SAMBA_VERSION="2:4.13.2+dfsg-3" \
    IPROUTE2_VERSION="5.9.0-1"

ENV BACKUPDIR=/backups
VOLUME /backups

RUN apt-get update && \
    apt-get --no-install-recommends --yes install \
        samba="$SAMBA_VERSION" \
        samba-vfs-modules="$SAMBA_VERSION" \
        iproute2=${IPROUTE2_VERSION} && \
    rm -rf /var/lib/apt/lists/*

ADD samba.conf /etc/samba/smb.conf
ADD TimeMachine.quota.tmpl /etc/TimeMachine.quota.tmpl

EXPOSE 445/tcp

ADD entrypoint /entrypoint
RUN chmod 0755 /entrypoint

ENTRYPOINT ["/entrypoint"]
