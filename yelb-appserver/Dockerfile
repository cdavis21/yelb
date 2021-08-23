FROM public.ecr.aws/bitnami/ruby:3.0.2-prod
MAINTAINER massimo@it20.info

################## BEGIN INSTALLATION ######################

# Set the working directory to /app
WORKDIR /app

COPY yelb-appserver.rb yelb-appserver.rb 
COPY Gemfile Gemfile
COPY modules modules

ENV LANG=en_us.UTF-8
ENV LC_ALL=C.UTF-8
ENV RACK_ENV=production

RUN gem install sinatra --no-document
RUN gem install redis --no-document

### hack to allow the setup of the pg gem (which would fail otherwise), todo:// review the update. Will cause issues if building for every env
RUN apt-get update
RUN apt-get install libpq-dev  build-essential -y
### end of hack (this would require additional research and optimization)

RUN gem install pg --no-document
RUN gem install aws-sdk-dynamodb --no-document
RUN gem install thin --no-document

# Set the working directory to /
WORKDIR /
ADD startup.sh startup.sh

##################### INSTALLATION END #####################

CMD ["./startup.sh"]


