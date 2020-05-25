FROM ruby:2.6.5

RUN apt-get update -qq && apt-get install -y \
    build-essential \
    nodejs \
    yarn \
 && rm -rf /var/lib/apt/lists/*

RUN gem install bundler

ENV APP_HOME /myapp
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

ADD package.json $APP_HOME/package.json
ADD yarn.lock $APP_HOME/yarn.lock
RUN yarn install

ADD Gemfile $APP_HOME/Gemfile
ADD Gemfile.lock $APP_HOME/Gemfile.lock
RUN bundle install

EXPOSE 3000

ADD . $APP_HOME
CMD ["bundle", "exec", "rails", "server", "-p", "3000", "-b", "0.0.0.0"]
