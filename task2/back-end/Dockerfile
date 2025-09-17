# Use the latest Ubuntu as base image
FROM ubuntu:latest

# Update APT package index
RUN apt-get update

# Upgrade currently installed software
RUN apt-get upgrade -y

# Install Python3 and pip3
RUN apt-get install -y python3 python3-pip

# Remove externally managed environment file to allow pip installations
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED

# Install Flask using pip3
RUN pip3 install flask

# Set working directory
WORKDIR /app

# Copy the Python API file to the container
COPY ./api.py /app/api.py

# Run the Flask application
CMD ["python3", "api.py"]
