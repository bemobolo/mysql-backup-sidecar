FROM debian:12-slim

LABEL maintainer="Wolfgang Gassler"
LABEL description="XtraBackup based MySQL / MariaDB backup docker image to create incremental backups periodically"

# installing xtrabackup according to https://docs.percona.com/percona-xtrabackup/8.4/apt-repo.html

RUN . /etc/os-release \
    && apt-get update \
    && apt-get -y install wget lsb-release gnupg2 cron curl \
    && rm -rf /etc/cron.* \
    && . /etc/os-release \
    && wget https://repo.percona.com/prel/apt/pool/testing/p/percona-release/percona-release_1.0-30.generic_all.deb \
    && dpkg -i percona-release_1.0-30.generic_all.deb \
    && rm -f percona-release_1.0-30.generic_all.deb \
    && apt-get update \
    && percona-release setup pxb84-lts \
    && apt-get -y install percona-xtrabackup-84 lz4

COPY scripts /scripts

VOLUME /backup /var/lib/mysql
WORKDIR /backup

CMD ["/scripts/start.sh"]