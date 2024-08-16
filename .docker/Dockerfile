FROM python:3.9-slim-buster

# Install necessary packages and clean up
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    pipx \
    python3-venv \
    && apt-get clean all \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry using pipx
RUN pipx install poetry==1.5.1

# Set the virtual environment path
ENV POETRY_VIRTUALENVS_IN_PROJECT=true
ENV POETRY_VIRTUALENVS_PATH=/project/.venv

# Set the working directory
WORKDIR /project

# Copy the project files
COPY . ./

# Install the project dependencies
RUN /root/.local/bin/poetry install

# Add the virtual environment to the PATH and source it
ENV PATH="/project/.venv/bin:$PATH"
RUN echo 'source /project/.venv/bin/activate' >> ~/.bashrc

# Default command to run when starting the container
# CMD ["bash"]
ENTRYPOINT ["python", "examples/user/ur5_example.py"]
