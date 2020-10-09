FROM golang:alpine AS builder

RUN apk update && apk add --no-cache git

WORKDIR $GOPATH/src/app

COPY . .

RUN go get -d -v
RUN go build -o /go/src/app

RUN GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/app

FROM scratch

COPY --from=builder /go/bin/app /go/bin/app

ENTRYPOINT  ["/go/bin/app"]
