FROM python:3.10-slim
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    libpcre3 \
    libpcre3-dev \
    && rm -rf /var/lib/apt/lists/*

# Install pipenv
RUN pip install --no-cache-dir pipenv

# Create necessary directories
RUN mkdir -p /var/www/app

# Install Python dependencies
COPY Pipfile Pipfile.lock ./
RUN pipenv install --system --deploy

# Copy application code
COPY . .

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "-s", "/var/www/app/app.sock", "--manage-script-name", "--mount", "/=app:app"]