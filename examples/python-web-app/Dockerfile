# Use a Python slim image
FROM python:3.12-slim

# Set environment variables
ENV PYTHONUNBUFFERED=1
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

# Install system dependencies
RUN apt-get update && apt-get install -y \
    python3-pip \
    python3-venv \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /app

# Copy requirements file
COPY requirements.txt .

# Install dependencies explicitly bypassing the restriction
RUN python3 -m venv /app/venv && \
    /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install --break-system-packages -r requirements.txt

# Add the virtual environment's bin directory to PATH
ENV PATH="/app/venv/bin:$PATH"

# Copy the rest of the application code
COPY . .

# Expose the port for the Django development server
EXPOSE 8000

# Run the application
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]



