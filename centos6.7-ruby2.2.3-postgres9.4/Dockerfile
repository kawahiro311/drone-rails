FROM centos:6.7

# Install packages for building ruby
RUN yum -y update
RUN yum install -y git gcc gcc-c++ make tar wget openssl-devel readline-devel sqlite-devel zlib zlib-devel file
RUN yum install -y libcurl-devel libyaml-devel libffi-devel bzip2 autoconf automake libtool bison libxml2-devel libxslt-devel
RUN yum clean all

# Install rbenv and ruby-build
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN ./root/.rbenv/plugins/ruby-build/install.sh
ENV PATH /root/.rbenv/bin:$PATH
RUN echo 'export PATH=/root/.rbenv/bin:$PATH' >> /root/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /root/.bashrc

# Install ruby
ENV CONFIGURE_OPTS --disable-install-doc
RUN rbenv install 2.2.3
RUN rbenv global 2.2.3

# Install Bundler for ruby
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN rbenv exec gem install bundler

# Install node.js
RUN rpm -ivh http://ftp.iij.ad.jp/pub/linux/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum -y install nodejs npm --enablerepo=epel
RUN yum clean all
RUN npm install -g bower

# Install postgres
RUN rpm -ivh http://yum.postgresql.org/9.4/redhat/rhel-6-x86_64/pgdg-centos94-9.4-1.noarch.rpm
RUN yum -y install postgresql94 postgresql94-devel postgresql94-server
RUN yum clean all
RUN ./etc/init.d/postgresql-9.4 initdb -E UNICODE --no-locale
COPY pg_hba.conf /var/lib/pgsql/9.4/data/pg_hba.conf
RUN echo "listen_addresses = '*'" >> /var/lib/pgsql/9.4/data/postgresql.conf

# Install packages for ImageMagick
RUN yum -y install libjpeg-devel libpng-devel
RUN yum -y install ImageMagick ImageMagick-devel
RUN yum clean all

# Install packages for poltergeist
RUN cd /usr/local/src/ && wget https://phantomjs.googlecode.com/files/phantomjs-1.9.2-linux-x86_64.tar.bz2
RUN tar jxfv /usr/local/src/phantomjs-1.9.2-linux-x86_64.tar.bz2
RUN cp phantomjs-1.9.2-linux-x86_64/bin/phantomjs /usr/bin/
