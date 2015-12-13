# centos6.7-ruby2.2.3-postgres9.4 docker image

## sample .drone.yml

```
build:
  image: kawahiro311/centos6.7-ruby2.3-postgres9.4
  commands:
    - service postgresql-9.4 start
    - export PATH=$PATH:/root/.rbenv/shims
    - bundle config build.nokogiri --use-system-libraries
    - bundle config build.pg --with-pg-config=/usr/pgsql-9.4/bin/pg_config
    - bundle install -j4
    - RAILS_ENV=test bundle exec rake db:create db:migrate
    - bundle exec rspec
```
