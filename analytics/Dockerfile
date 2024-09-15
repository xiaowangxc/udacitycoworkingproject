FROM python:3.8-slim-buster

WORKDIR /src

COPY ./requirements.txt requirements.txt

RUN apt update -y && apt install build-essential libpq-dev -y
RUN pip install --upgrade pip setuptools wheel
RUN pip install werkzeug==2.2.2
RUN pip install -r requirements.txt
RUN kubectl port-forward service/postgresql-service 5433:5432 &

ENV DB_USERNAME=myuser DB_PASSWORD=mypassword DB_HOST=127.0.0.1 DB_PORT=5433 DB_NAME=mydatabase

COPY . .

CMD python app.py