# Variables for plugins
PROTOC_GEN_GO := $(shell where protoc-gen-go)
PROTOC_GEN_GO_GRPC := $(shell where protoc-gen-go-grpc)

# Default target
all: generate build

# Install protoc-gen-go if missing
install-protoc-gen-go:
ifndef PROTOC_GEN_GO
	@echo "Installing protoc-gen-go..."
	go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
else
	@echo "protoc-gen-go is already installed."
endif

# Install protoc-gen-go-grpc if missing
install-protoc-gen-go-grpc:
ifndef PROTOC_GEN_GO_GRPC
	@echo "Installing protoc-gen-go-grpc..."
	go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
else
	@echo "protoc-gen-go-grpc is already installed."
endif

# Install all dependencies
install-deps: install-protoc-gen-go install-protoc-gen-go-grpc

# Generate code from .proto files
generate: install-deps
	@echo "Generating code from .proto files for OrdersManagement..."
	protoc --proto_path=../shared/proto \
           --go_out=./internal/proto \
           --go_opt=Morder.proto=./ \
           --go-grpc_out=./internal/proto \
           --go-grpc_opt=Morder.proto=./ \
           --go-grpc_opt=paths=source_relative \
           order.proto

# Build the project
build:
	@echo "Building the project..."
	go build -o bin/OrdersManagement cmd/main.go

# Run the project
run:
	@echo "Running the project..."
	go run cmd/main.go

# Run tests
test:
	@echo "Running tests..."
	go test -v ./...

# Migrations (stub, add your logic)
migrate:
	@echo "Running migrations..."
	# Add commands for migrations, for example:
	# goose -dir ./migrations postgres "user=postgres dbname=mydb sslmode=disable" up

# Clean generated files
clean:
	@echo "Cleaning generated files..."
	rm -rf ./internal/proto/*.pb.go

# Help (list available commands)
help:
	@echo "Available commands:"
	@echo "  make all               - Install dependencies, generate code, and build the project (default)."
	@echo "  make install-deps      - Install all required dependencies."
	@echo "  make generate          - Generate code from .proto files."
	@echo "  make build            - Build the project."
	@echo "  make run              - Run the project."
	@echo "  make test             - Run tests."
	@echo "  make migrate          - Run migrations (add your logic)."
	@echo "  make clean            - Clean generated files."
	@echo "  make help             - Show this message."

.PHONY: all install-deps install-protoc-gen-go install-protoc-gen-go-grpc generate build run test migrate clean help