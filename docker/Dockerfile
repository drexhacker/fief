FROM python:3.12-slim

ENV PYTHONUNBUFFERED 1

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y build-essential redis libpq-dev nodejs npm \
    && pip install --upgrade pip \
    && python --version \
    && apt-get autoremove -y build-essential \
    && mkdir -p /data/db \
    && mkdir -p /run/secrets

# Copy the entire project directory
COPY . /app/fief

# Install Python dependencies
RUN pip install hatch

# Install Node.js dependencies
WORKDIR /app/fief
RUN npm ci

# Compile translations and build assets
RUN hatch run translations.compile && \
    hatch run static.build

# Install the local Fief package
RUN pip install .

ENV DATABASE_LOCATION=/data/db
ENV SECRETS_DIR /run/secrets

ENV PORT=8000
EXPOSE ${PORT}