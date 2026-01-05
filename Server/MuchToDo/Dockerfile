# ---------- Build Stage ----------
FROM golang:1.22-alpine AS builder
ENV GOTOOLCHAIN=auto

WORKDIR /app

# Copy go mod files first (cache dependencies)
COPY go.mod go.sum ./
RUN go mod download

# Copy source code
COPY . .

# Build the application
# IMPORTANT: main.go is in cmd/api
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
  go build -o app ./cmd/api

# ---------- Runtime Stage ----------
FROM alpine:3.19

# Create non-root user
RUN adduser -D appuser

WORKDIR /app

# Copy binary from builder
COPY --from=builder /app/app .
COPY .env.example .env

EXPOSE 8080

USER appuser

HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -qO- http://localhost:8080/health || exit 1

CMD ["./app"]
