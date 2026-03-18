# BUILDER
FROM python:3.8-bullseye AS builder

WORKDIR /app

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    gcc \
    libxml2-dev \
    libxslt-dev \
    python3-dev \
    build-essential \
    zlib1g-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# RUNTIME
FROM python:3.8-slim

WORKDIR	/app

COPY --from=builder /usr/local /usr/local

COPY . .

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
