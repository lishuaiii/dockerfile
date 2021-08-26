FROM golang:1.15-alpine3.12 as builder

ARG goproxy

COPY . /go/src/github.com/flike/kingshard
RUN cd /go/src/github.com/flike/kingshard \
  && GO111MODULE=off GOPROXY=$goproxy GOOS=linux CGO_ENABLED=0 go install -v ./vendor/golang.org/x/tools/cmd/goyacc \
  && /go/bin/goyacc -o ./sqlparser/sql.go ./sqlparser/sql.y \
  && GO111MODULE=off GOPROXY=$goproxy GOOS=linux CGO_ENABLED=0 go install -v ./cmd/kingshard

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
  && apk --update add --no-cache tzdata git

FROM scratch

COPY --from=builder /usr/share/zoneinfo /usr/share/zoneinfo
COPY --from=builder /etc/passwd /etc/
COPY --from=builder /go/bin/kingshard /bin/

WORKDIR /

# server listen addr
EXPOSE 3306
# the web api server
EXPOSE 9797

USER nobody

ENTRYPOINT ["/bin/kingshard"]

