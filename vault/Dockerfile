############################################################
# Dockerfile to create a Hashicorp Vault dev server image
# Based on work demonstrated in voxxit's vault Dockerfile
############################################################
# Use the Alpine minimal image
FROM library/alpine:latest

MAINTAINER Doug Rockney "drockney@gmail.com"

RUN apk update && apk upgrade && apk add curl \
    && curl https://releases.hashicorp.com/vault/0.5.2/vault_0.5.2_linux_amd64.zip -o vault_0.5.2_linux_amd64.zip \
    && apk del curl && unzip vault_0.5.2_linux_amd64.zip \
    && mv vault /usr/local/bin/ && rm -f vault_0.5.2_linux_amd64.zip

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
