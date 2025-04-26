# Use the official Python base image (Use stable version - 3.13 is not yet stable as of 2025)
FROM python:3.12-alpine

# Set working directory inside container
WORKDIR /app

# Copy only requirements.txt first to leverage Docker caching
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application files
COPY . .

# Expose port (Flask app runs on 5000)
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]
