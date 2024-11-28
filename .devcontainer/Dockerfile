# Start with a Python 3.9 slim base image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements.txt file into the container
COPY requirements.txt .

# Install dependencies from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code into the container
COPY service/ ./service/

# Create a non-root user named 'theia'
RUN useradd --uid 1000 theia && chown -R theia /app

# Switch to the 'theia' user for better security
USER theia

# Expose port 8080 to allow external access
EXPOSE 8080

# Command to run the application using Gunicorn
CMD ["gunicorn", "--bind=0.0.0.0:8080", "--log-level=info", "service:app"]
