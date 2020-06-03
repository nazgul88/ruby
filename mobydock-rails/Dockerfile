FROM ruby:2.3.8-slim-jessie
LABEL maintainer="Nick Janetakis <nick.janetakis@gmail.com>"

RUN apt-get update && apt-get install -qq -y \
  build-essential nodejs libpq-dev --fix-missing --no-install-recommends

WORKDIR /app

COPY Gemfile* ./
RUN bundle install

COPY . .

RUN bundle exec rake RAILS_ENV=production DATABASE_URL=postgresql://user:pass@127.0.0.1/dbname SECRET_TOKEN=pickasecuretoken assets:precompile

VOLUME ["/app/public"]

CMD bundle exec unicorn -c config/unicorn.rb
