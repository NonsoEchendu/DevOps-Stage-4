# Stage 1: Build the Go application
FROM golang:1.21 AS build-stage

# Set the working directory
WORKDIR /app

# Copy go.mod and go.sum to download dependencies
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-api ./cmd/auth-api

# Stage 2: Create a minimal runtime image
FROM alpine:3.19

# Set the working directory
WORKDIR /app

# Copy the built binary from the build stage
COPY --from=build-stage /app/auth-api .

# Copy the .env file from root directory
COPY ../.env .

# Expose port
EXPOSE 8081

# Set environment variables from .env file
ENV $(grep -v '^#' .env | xargs)

# Run the application
CMD ["./auth-api"]