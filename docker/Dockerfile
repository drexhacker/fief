FROM python:3.12-slim

ENV PYTHONUNBUFFERED 1

WORKDIR /app

RUN apt-get update && apt-get install -y build-essential libpq-dev \
    && pip install --upgrade pip \
    && python --version \
    && apt-get autoremove -y build-essential \
    && mkdir -p /data/db

# Copy the entire project directory
COPY . /app/fief

# Install the local Fief package in editable mode
RUN pip install /app/fief

ENV DATABASE_LOCATION=/data/db
ENV SECRETS_DIR /run/secrets

ENV PORT=8000
EXPOSE ${PORT}