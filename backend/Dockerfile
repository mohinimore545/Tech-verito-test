# backend/Dockerfile
# Build stage
FROM golang:1.19 AS builder
WORKDIR /app
# Use modules
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o server main.go

# Final stage
FROM gcr.io/distroless/static:nonroot
WORKDIR /app
COPY --from=builder /app/server /app/server
USER nonroot:nonroot
EXPOSE 8080
ENTRYPOINT ["/app/server"]
