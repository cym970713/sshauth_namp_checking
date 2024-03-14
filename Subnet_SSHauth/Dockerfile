# Use a base image with Python 3.10
FROM python:3.10

# Set up proxy environment variables
#ARG HTTP_PROXY=http://
#ARG HTTPS_PROXY=http://
#ENV http_proxy=$HTTP_PROXY
#ENV https_proxy=$HTTPS_PROXY

#Set the timezone to Malaysia (KL)
ENV TZ=Asia/Kuala_Lumpur

# Update the package repository and install nmap
RUN apt-get update && \
    apt-get install -y nmap

# Copy your script into the container
COPY . /app

# Set the working directory
WORKDIR /app

# Install any additional dependencies if needed
RUN pip install -r requirement.txt

# Define the command to run your script and copy to shared volumn
CMD ["python", "nmapscanning_subnet.py"]


