# Using Debian's GCC image, pinned to latest LTS, scheduled to EOL on Jun'26.
FROM cimg/base:current-18.04 as builder

ARG DEBIAN_FRONTEND=noninteractive

# Package 'lsb-release' is required by 'percona-release' package.
RUN \
  sudo apt-get update && \
  sudo apt-get remove libmariadb-dev && \
  sudo apt-get install -y lsb-release cmake g++ git make libglib2.0-dev zlib1g-dev libpcre3-dev libpcre2-dev libssl-dev libzstd-dev wget gnupg curl && \
  sudo apt-get clean

RUN \
  . /etc/os-release && \
  curl --fail --location --show-error --silent --output /tmp/percona-release.deb \
    https://repo.percona.com/apt/percona-release_latest.${VERSION_CODENAME}_all.deb && \
  sudo dpkg -i /tmp/percona-release.deb && \
  rm -v /tmp/percona-release.deb && \
  sudo apt-get update && \
  sudo apt-get clean

RUN \
  wget https://r.mariadb.com/downloads/mariadb_repo_setup -O /tmp/mariadb_repo_setup


