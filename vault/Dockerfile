############################################################
# Dockerfile to create a Hashicorp Vault dev server image
# Based on work demonstrated in voxxit's vault Dockerfile
############################################################
# Use the Alpine minimal image
FROM library/alpine:latest

MAINTAINER Doug Rockney "drockney@gmail.com"

# We need curl to retrieve https content, wget in Alpine's
# BusyBox won't support SSL retrieval.
RUN apk update && apk upgrade && apk add curl
RUN curl https://releases.hashicorp.com/vault/0.5.2/vault_0.5.2_linux_amd64.zip -o vault_0.5.2_linux_amd64.zip
# OK, done with Curl, now we can remove it
RUN apk del curl

# Unpack Vault clean up
RUN unzip vault_0.5.2_linux_amd64.zip
RUN mv vault /usr/local/bin/
RUN rm -f vault_0.5.2_linux_amd64.zip

# Vault uses port 8200 for communications.
EXPOSE 8200

# By default, Vault tries to start in TLS mode.  Let's tell
# it that it's a dev instance only and not to use TLS.
# That way, using "vault status" will work.
ENV VAULT_ADDR='http://127.0.0.1:8200'

# Run Vault in dev mode, which means it's by default
# using an unsealed in-memory vault that will be lost
# when the container is shut down.  Don't use this in
# production!
ENTRYPOINT [ "vault" ]
CMD [ "server", "-dev" ]