# Copyright 2019 gRPC authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM php:5.6-zts-stretch

RUN apt-get -qq update && apt-get -qq install -y \
  autoconf automake git libtool pkg-config \
  valgrind wget zlib1g-dev


WORKDIR /tmp

RUN wget https://phar.phpunit.de/phpunit-4.8.36.phar && \
  mv phpunit-4.8.36.phar /usr/local/bin/phpunit && \
  chmod +x /usr/local/bin/phpunit


WORKDIR /github/grpc

RUN git clone https://github.com/grpc/grpc . && \
  git submodule update --init

COPY src/ ./src

RUN pear package && \
  find . -name grpc-*.tgz | xargs -I{} pecl install {}


CMD ["/github/grpc/src/php/bin/run_tests.sh", "--skip-persistent-channel-tests"]
