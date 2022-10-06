#Alpine x64
FROM loadimpact/k6:latest AS k6official

FROM mcr.microsoft.com/dotnet/runtime-deps:6.0.6-alpine3.16-amd64 as initial
#RUN apk add bash icu-libs krb5-libs libgcc libintl libssl1.1 libstdc++ zlib #if using base alpine above 3.9
#RUN apk add libgdiplus --repository https://dl-3.alpinelinux.org/alpine/edge/testing/ #optional

WORKDIR /app
COPY . .
RUN chmod +x ./AppWeb.Machine

RUN apk upgrade --no-cache --available && \
    apk add curl && \
    rm -rf /var/cache/apk/*

RUN curl -L https://fly.io/install.sh | sh

FROM mcr.microsoft.com/dotnet/runtime-deps:6.0.6-alpine3.16-amd64
WORKDIR /app

#RUN addgroup --system --gid 101 app \
#    && adduser --system --ingroup app --uid 101 app
#USER app
#COPY --from=initial --chown=app:app /app /app
COPY --from=initial /app /app
COPY --from=initial /root/.fly /root/.fly
COPY --from=k6official /usr/bin/k6 /usr/bin/k6

ENV FLYCTL_INSTALL="/root/.fly"
ENV PATH="$FLYCTL_INSTALL/bin:$PATH"

EXPOSE 8080
EXPOSE 9091

CMD ["./AppWeb.Machine", "--urls", "http://0.0.0.0:8080;http://0.0.0.0:9091"]

