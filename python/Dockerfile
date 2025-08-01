# Define the base of your image.
# Specifying `--platform=linux/amd64` ensures compatibility when building on Apple Silicon (M1/M2).
# Always pin the version (e.g., python:3.10-slim) to ensure reproducibility.
FROM --platform=linux/amd64 python:3.10-slim

# Install essential build tools such as gcc/g++ that may be needed to compile certain Python packages.
RUN apt-get update && \
    apt-get install -y build-essential gcc g++ && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory for the COPY, RUN, and ENTRYPOINT commands.
WORKDIR /home/user

# Copy all files from the build context into the image.
COPY . .

# Install Python dependencies listed in requirements.txt.
# Use --no-cache-dir to reduce image size, and --break-system-packages to allow installation
# even if it modifies system-managed packages (use cautiously).
RUN pip install \
    --no-cache-dir \
    --break-system-packages \
    -r requirements.txt

# Set the main command to run your model script when the container starts.
ENTRYPOINT ["python", "run_model.py"]

