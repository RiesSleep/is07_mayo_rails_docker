FROM mysql:5.7.21
LABEL  maintainer "k-waragai <kazuxtuna@gmail.com>"

# Initial command
RUN apt-get update && \
    apt-get install -y apt-utils locales

RUN rm -rf /var/lib/apt/lists/*

# Charset
ADD ./docker/mysql/my.cnf /etc/my.cnf
