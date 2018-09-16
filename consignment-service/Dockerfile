FROM golang:1.9.0 as builder

WORKDIR /go/src/shipper/consignment-service

COPY . .

RUN go get -u github.com/golang/dep/cmd/dep

RUN dep init && dep ensure

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .

FROM debian:latest

RUN apt-get update && apt-get install -y ca-certificates

RUN mkdir /app
WORKDIR /app

COPY --from=builder /go/src/shipper/consignment-service/consignment-service .

CMD ["./consignment-service"]