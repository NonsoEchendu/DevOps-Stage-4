# Use Python 3 as the base image
FROM python:3

# Set the working directory
WORKDIR /app

# Copy requirements.txt
COPY requirements.txt .

# Install dependencies
RUN pip3 install -r requirements.txt

# Copy the rest of the application code
COPY . .

# Copy the .env file from the parent directory
COPY ../.env .

# Set environment variables from .env file
ENV $(grep -v '^#' .env | xargs)

# Run the application
CMD ["sh", "-c", "python3 main.py"]