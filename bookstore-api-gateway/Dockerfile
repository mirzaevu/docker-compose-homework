FROM golang:1.23-alpine AS builder

WORKDIR /app

COPY . .

RUN rm -f go.mod go.sum

RUN go mod init github.com/nvrbckdown/bookstore-api-gateway
RUN go get github.com/gin-gonic/gin
RUN go get github.com/gin-contrib/cors@v1.4.0
RUN go get github.com/joho/godotenv
RUN go get github.com/sirupsen/logrus
RUN go get github.com/golang-jwt/jwt/v5
RUN go mod tidy

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o api-gateway ./cmd/server

FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/api-gateway .

EXPOSE 8080

CMD ["./api-gateway"]
