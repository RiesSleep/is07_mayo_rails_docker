FROM ruby:2.5.1
LABEL  maintainer "k-waragai <kazuxtuna@gmail.com>"

# Initial command
RUN apt-get update -qq && \
    apt-get install -y build-essential libpq-dev nodejs

# WORKDIR ENV
ENV work_dir /rails_app

# Rails setting
RUN mkdir ${work_dir}
WORKDIR ${work_dir}

COPY ./Gemfile /${work_dir}/Gemfile
COPY ./Gemfile.lock /${work_dir}/Gemfile.lock
RUN bundle install

# sockets dir setting
RUN mkdir -p ${work_dir}/tmp/sockets

COPY . ${work_dir}
