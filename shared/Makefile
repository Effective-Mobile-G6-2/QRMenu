# Variables
GOOGLEAPIS_DIR := third_party/googleapis

# Default target
all: download-googleapis

# Download googleapis repository
download-googleapis:
	@echo Downloading googleapis...
	@if not exist "$(GOOGLEAPIS_DIR)" ( \
		git clone https://github.com/googleapis/googleapis.git $(GOOGLEAPIS_DIR) \
	) else ( \
		echo googleapis already downloaded. \
	)

# Clean downloaded files
clean:
	@echo Cleaning downloaded files...
	@if exist "$(GOOGLEAPIS_DIR)" rmdir /s /q "$(GOOGLEAPIS_DIR)"

# Help (list available commands)
help:
	@echo Available commands:
	@echo   make all               - Download required dependencies (default).
	@echo   make download-googleapis - Download googleapis repository.
	@echo   make clean             - Clean downloaded files.
	@echo   make help              - Show this message.

.PHONY: all download-googleapis clean help