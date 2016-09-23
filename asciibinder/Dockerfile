FROM alpine:3.4

MAINTAINER Doug Rockney "drockney@gmail.com"

RUN apk update && \
    apk add musl-dev openjdk7 && \
    apk add make gcc g++ git && \
    apk add ruby ruby-dev ruby-rdoc ruby-irb && \
    apk add libffi libffi-dev && \
    gem install listen && \
    gem install ascii_binder && \
    gem install io-console && \
    rm -rf /var/cache/apk

LABEL url="http://www.asciibinder.org" \
      summary="a documentation system built on Asciidoctor" \
      description="AsciiBinder is for documenting versioned, interrelated projects. Run this container image from the documentation repository, which is mounted into the container. Note: Generated files will be owned by root." \
      RUN="docker run -it --rm \
          -v `pwd`:/docs:z \
          IMAGE"

ENV JAVA_HOME=/usr/lib/jvm/java-1.7-openjdk/jre/
ENV LANG=en_US.UTF-8
WORKDIR /docs
CMD asciibinder package

