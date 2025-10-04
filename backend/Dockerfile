FROM python:3.12

WORKDIR /app

RUN pip install gunicorn==23.0.0
RUN pip install --upgrade pip setuptools

COPY requirements.txt .
RUN pip install -r requirements.txt --no-cache-dir

COPY . .

# Создаем директории для статики и медиа
RUN mkdir -p staticfiles media

# Собираем статические файлы (включая DRF)
RUN python manage.py collectstatic --noinput --clear

CMD ["gunicorn", "kittygram_backend.wsgi:application", "--bind", "0.0.0.0:8000"]