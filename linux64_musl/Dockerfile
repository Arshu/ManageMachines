#Alpine x64
FROM mcr.microsoft.com/dotnet/runtime-deps:6.0.6-alpine3.16-amd64 as initial

WORKDIR /app

COPY . .
RUN chmod +x ./AppWeb.Machine

RUN apk upgrade --no-cache --available && \
    apk add curl && \
    rm -rf /var/cache/apk/*

RUN curl -L https://fly.io/install.sh | sh

FROM mcr.microsoft.com/dotnet/runtime-deps:6.0.6-alpine3.16-amd64
WORKDIR /app
COPY --from=initial /app /app
COPY --from=initial /root/.fly /root/.fly

ENV FLYCTL_INSTALL="/root/.fly"
ENV PATH="$FLYCTL_INSTALL/bin:$PATH"

EXPOSE 8080
EXPOSE 9091

CMD ["./AppWeb.Machine", "--urls", "http://0.0.0.0:8080;http://0.0.0.0:9091"]

