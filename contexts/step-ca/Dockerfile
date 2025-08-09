FROM alpine:3.21
WORKDIR /app

ENV STEP=/home/step
ENV STEPPATH=/home/step

COPY entrypoint.sh /entrypoint.sh
RUN apk add --no-cache bash

ADD step_linux.tar.gz step/
RUN ln -s "/app/step/step_0.28.6/bin/step" "/usr/local/bin/step"

ADD step-ca_linux.tar.gz step-ca/
RUN ln -s "/app/step-ca/step-ca" "/usr/local/bin/step-ca"

RUN adduser -s "/bin/ash" -h "/home/step" -D step
USER step
RUN mkdir "/home/step/.step"

ENV CONFIGPATH="/home/step/config/ca.json"
ENV PWDPATH="/home/step/secrets/password"

VOLUME ["/home/step"]
STOPSIGNAL SIGTERM
HEALTHCHECK CMD step ca health 2>/dev/null | grep "^ok" >/dev/null

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
CMD exec /usr/local/bin/step-ca --password-file $PWDPATH $CONFIGPATH
