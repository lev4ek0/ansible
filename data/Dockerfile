FROM python:3.8
ENV PYTHONBUFFERED 1
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
RUN python3 manage.py makemigrations && python3 manage.py migrate && python3 manage.py collectstatic --noinput && python3 manage.py test
EXPOSE 80
CMD ["gunicorn", "--bind", ":80", "--workers", "3", "locallibrary.wsgi:application"]