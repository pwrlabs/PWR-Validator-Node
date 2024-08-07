# Use a minimal Ubuntu base image
FROM ubuntu:20.04

# Install OpenJDK and wget
RUN apt-get update && \
    apt-get install -y openjdk-21-jre-headless wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /app

# Download the validator.jar and config.json
RUN wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/validator.jar && \
    wget https://github.com/pwrlabs/PWR-Validator-Node/raw/main/config.json

# Copy the password file into the container
COPY password /app/password

# Expose the necessary ports
EXPOSE 8231
EXPOSE 8085
EXPOSE 7621/udp

# Set the environment variable for SERVER_IP, default to 0.0.0.0
ENV SERVER_IP=0.0.0.0

# Run the application
CMD ["sh", "-c", "java -jar validator.jar password $SERVER_IP --compression-level 0"]