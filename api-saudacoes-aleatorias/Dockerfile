FROM golang:1.24-alpine AS builder

RUN apk add --no-cache build-base gcc

WORKDIR /app

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=1 GOOS=linux go build -a -installsuffix cgo -o /app/main .

FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/main .

EXPOSE 8080

CMD ["./main"]