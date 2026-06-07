# Option: golang:1.22-alpine + Multi-stage (produces tiny ~10MB image)
FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

FROM scratch
COPY --from=builder /app/main /main
EXPOSE 8080
CMD ["/main"]