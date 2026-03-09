FROM python:3.10
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

# Install pipenv
RUN pip install --no-cache-dir pipenv

# Create necessary directories
RUN mkdir -p /var/www/app

# Install Python dependencies
COPY Pipfile Pipfile.lock ./
RUN pipenv install --system --deploy

# Copy application code
COPY . .

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "--pythonpath", "/", "--manage-script-name", "--mount", "/=app:app"]