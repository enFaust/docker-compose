# Multi-stage Dockerfile for Python Flask application

# Build stage
FROM python:3.9-slim as build

# Set working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt .

# Install dependencies
RUN pip install --user -r requirements.txt

# Runtime stage
FROM python:3.9-slim as runtime

# Copy installed packages from build stage
COPY --from=build /root/.local /root/.local

# Copy application code
COPY app.py .

# Set environment variables
ENV PATH=/root/.local/bin:$PATH

# Expose port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]