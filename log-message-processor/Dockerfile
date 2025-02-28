# Use Python 3 as the base image
FROM python:3.9

# Set the working directory
WORKDIR /app

# Copy requirements.txt
COPY requirements.txt .

# Install dependencies, excluding py_zipkin
RUN grep -v "py_zipkin" requirements.txt | pip install -r /dev/stdin

# Install py_zipkin v0.20.0 explicitly
RUN pip install py_zipkin==0.20.0

# Copy the rest of the application code
COPY . .

# Run the application
CMD ["sh", "-c", "python3 main.py"]
