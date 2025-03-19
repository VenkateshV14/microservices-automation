FROM golang:1.22-alpine AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

RUN go build -o products-catalog .

FROM alpine AS release

WORKDIR /usr/src/app

COPY ./products ./products

COPY --from=builder /usr/src/app/products-catalog .

ENV PRODUCT_CATALOG_PORT 8088

ENTRYPOINT [ "./products-catalog" ]
