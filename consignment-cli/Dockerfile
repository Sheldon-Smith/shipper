FROM golang:1.9.0 as builder

WORKDIR /go/src/shipper/consignment-cli

COPY . .

RUN go get -u github.com/golang/dep/cmd/dep

RUN dep init && dep ensure

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .

FROM debian:latest

RUN apt-get update && apt-get install -y ca-certificates

RUN mkdir -p /app
WORKDIR /app

ADD consignment.json /app/consignment.json
ADD consignment-cli /app/consignment-cli

COPY --from=builder /go/src/shipper/consignment-cli/consignment-cli .

CMD ["./consignment-cli"]