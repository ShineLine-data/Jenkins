FROM python:3.13-slim
EXPOSE 8000
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
COPY requirements.txt .
RUN python -m pip install -r requirements.txt
WORKDIR /app
COPY . /app/
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown appuser /app
USER appuser
CMD [ "gunicorn", "--bind", "0.0.0.0:8000", "odc.wsgi:application" ]