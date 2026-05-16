FROM python:3.11-slim

WORKDIR /app

# Install all system dependencies for Pillow, psycopg2, and other libraries
RUN apt-get update && apt-get install -y \
    gcc \
    g++ \
    make \
    postgresql-client \
    libpq-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libfreetype6-dev \
    libwebp-dev \
    libtiff5-dev \
    libopenjp2-7-dev \
    zlib1g-dev \
    libxcb1-dev \
    libxext-dev \
    libxrender-dev \
    libgomp1 \
    libatlas-base-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "kittygram_backend.wsgi"]
