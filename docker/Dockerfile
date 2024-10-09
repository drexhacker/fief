FROM python:3.12-slim

ARG FIEF_VERSION
ENV PYTHONUNBUFFERED 1

WORKDIR /app

RUN apt-get update && apt-get install -y build-essential redis libpq-dev \
    && pip install --upgrade pip supervisor \
    && python --version \
    && apt-get autoremove -y build-essential \
    && mkdir -p /data/db
    
# Copy your local Fief codebase
COPY . /app/fief/

# Install your local Fief package
RUN pip install -e /app/fief/
    
COPY supervisord.conf /etc/supervisord.conf

ENV DATABASE_LOCATION=/data/db
ENV SECRETS_DIR /run/secrets

ENV PORT=8000
EXPOSE ${PORT}

CMD ["docker/supervisord", "-c", "/etc/supervisord.conf"]
