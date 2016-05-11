FROM seblegall/php-docker:7.0
MAINTAINER Sébastien Le Gall <seb@le-gall.net>

ENV NODEJS_VERSION 0.12

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    echo "deb https://deb.nodesource.com/node_$NODEJS_VERSION jessie main" > /etc/apt/sources.list.d/nodesource.list && \
    echo "deb-src https://deb.nodesource.com/node_$NODEJS_VERSION jessie main" >> /etc/apt/sources.list.d/nodesource.list

RUN apt-get update && apt-get install -y \
    libaio1

# Install NodeJS and NPM packages
RUN apt-get install -y nodejs

RUN npm update -g && \
    npm install -g bower grunt-cli gulp

RUN apt-get install -y \
    python \
    python-dev \
    python-pip

RUN apt-get update && apt-get install -y \
    mysql-client \
    postgresql-client

RUN apt-get install -y \
    supervisor \
    vim \
    emacs \
    ftp \
    bash-completion \
    ack-grep \
    tofrodos \
    libssl-dev \
    zlib1g \
    zlib1g-dev \
    libyaml-dev \
    libxml2-dev \
    libxslt1-dev \
    libcurl4-openssl-dev \
    libreadline-dev

ENV RUBY_VERSION 2.3.0
ENV RUBY_FULL_VERSION 2.3.0

# install ruby
RUN wget http://cache.ruby-lang.org/pub/ruby/ruby-$RUBY_FULL_VERSION.tar.gz && \
    tar -xzf ruby-$RUBY_FULL_VERSION.tar.gz && \
    cd ruby-$RUBY_FULL_VERSION && \
    ./configure && \
    make && \
    make install && \
    cd ..  && \
    rm -rf ruby-$RUBY_FULL_VERSION ruby-$RUBY_FULL_VERSION.tar.gz

RUN pip install \
    git-app-version==0.4.0

RUN gem update --no-rdoc --no-ri  && \
    gem install --no-rdoc --no-ri \
    bundler \
    capistrano \
    capistrano-symfony \
    capistrano-composer \
    capistrano-npm \
    capistrano-gitinfos:0.1.0

RUN npm install -g phantomjs-prebuilt

RUN apt-get install -y graphviz

RUN apt-get install -y \
    ant \
    openjdk-7-jdk

RUN DEBIAN_FRONTEND=noninteractive apt-get install locales && \
    echo "fr_FR.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

ENV LANG fr_FR.UTF-8
ENV LANGUAGE fr_FR.UTF-8
ENV LC_ALL fr_FR.UTF-8

COPY config/.bashrc /root/.bashrc
COPY config/.bash_aliases /root/.bash_aliases
COPY config/.gitignore /root/.gitignore
COPY config/.gitconfig /root/.gitconfig

COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY docker-entrypoint.sh /entrypoint.sh

RUN chmod a+x /entrypoint.sh && chown root:root /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/bin/supervisord"]
