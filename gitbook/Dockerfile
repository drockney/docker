FROM alpine:latest
##############################################################################
# GitBook server
# Note: although you can "init" using this container, there is no Calibre
# install included (image size and glibc compatibility concerns) so there's no
# possibility of many output methods beyond website display.
#
# To use the container properly, do this at a minimum:
# docker run -d -p 4000:4000 -v /home/yourname/yourbook:/gitbook <imagename>
#
# You should then be able to open a browser and hit the website on port 4000.
# Any contents you change in /home/yourname/yourbook will automatically be
# seen and updated by GitBook.

MAINTAINER Doug Rockney "drockney@gmail.com"

# Update the updater, add necessary libraries, install the CLI toolchain,
# and then tell GitBook to run its own install routines.
RUN apk update && apk upgrade && \
    apk add git wget python nodejs && \
    npm install -g gitbook-cli && \
    gitbook install 2.6.7 && \
    mkdir /gitbook

# Clean up the package cache to reduce image size.
RUN rm -rf /var/cache/apk/*

WORKDIR /gitbook
EXPOSE 4000

# The default command is to run the HTML server.
CMD ["gitbook", "serve", "/gitbook"]
# You can also initialize a directory to start writing a book by running:
# docker run --rm -v /home/yourname/yourbook:/gitbook <imagename> gitbook init /gitbook
# See the GitBook documentation for more information on the toolset, but
# please remember that since Calibre isn't installed you're really limited
# to basic functionality.