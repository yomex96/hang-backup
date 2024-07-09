# # Use an official Python runtime as the base image
# FROM python:3.9-slim

# # Set the working directory inside the container
# WORKDIR /app

# # Copy the requirements.txt file to the container
# COPY requirements.txt .

# # Install dependencies from requirements.txt
# RUN pip install -r requirements.txt

# # Copy the entire application source code to the container
# COPY . .

# # Expose port 8000 for FastAPI
# EXPOSE 8000

# # Command to run the FastAPI server when the container starts
# CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]


# # Use an official Python runtime as the base image
# FROM python:3.9-slim

# # Set the working directory
# WORKDIR /app

# # Copy the requirements file
# COPY requirements.txt .

# # Install dependencies
# RUN pip install --no-cache-dir -r requirements.txt uvicorn[standard]==0.24.0.post1

# # Copy the rest of the application source code
# COPY . .

# # Expose port 8000
# EXPOSE 8000

# # Start FastAPI using uvicorn
# CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

# Use the official Python image from the Docker Hub
FROM python:3.10-slim AS base

# Set the working directory
WORKDIR /app

# Install Poetry
RUN pip install poetry

# Copy only the requirements to cache them in docker layer
COPY poetry.lock pyproject.toml /app/

# Install dependencies
RUN poetry config virtualenvs.create false && poetry install --no-dev

# Copy the rest of the application
COPY . /app

# Run the application
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]


