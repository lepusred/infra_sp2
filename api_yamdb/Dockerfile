FROM python:3.7-slim
WORKDIR /app
COPY requirements.txt ./
RUN python -m pip install --upgrade pip wheel
RUN pip install -r /app/requirements.txt --no-cache-dir
COPY ./ ./
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000"]