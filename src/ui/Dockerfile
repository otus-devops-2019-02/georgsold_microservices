FROM alpine:3.9 AS build
RUN apk -U update \
    && apk add --virtual build-dependencies \
        build-base \
    && apk add ruby-full ruby-dev \
    && gem install bundler:1.17.2 --no-ri --no-rdoc

ENV APP_HOME /app
RUN mkdir $APP_HOME

WORKDIR $APP_HOME
ADD Gemfile* $APP_HOME/
RUN bundle install

FROM alpine:3.9
RUN apk -U update \
    && apk add ruby-full

ENV APP_HOME /app

WORKDIR $APP_HOME

COPY --from=build /usr/lib/ruby /usr/lib/ruby
COPY --from=build /$APP_HOME /$APP_HOME
COPY --from=build \ 
/usr/bin/j2bson \
/usr/bin/tilt \
/usr/bin/b2json \
/usr/bin/rackup \
/usr/bin/puma \
/usr/bin/pumactl \
/usr/bin/haml \
/usr/bin/

ADD . $APP_HOME

ENV POST_SERVICE_HOST post
ENV POST_SERVICE_PORT 5000
ENV COMMENT_SERVICE_HOST comment
ENV COMMENT_SERVICE_PORT 9292

CMD ["puma"]
