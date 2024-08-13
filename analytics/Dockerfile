FROM python:3.8-slim-buster

WORKDIR /src

COPY ./requirements.txt requirements.txt

RUN apt update -y && apt install build-essential libpq-dev -y
RUN pip install --upgrade pip setuptools wheel
RUN pip install werkzeug==2.2.2
RUN pip install -r requirements.txt
RUN kubectl port-forward service/postgresql-service 5433:5432 &
RUN export DB_USERNAME=myuser && export DB_PASSWORD=mypassword && export DB_HOST=127.0.0.1 && export DB_PORT=5433 && export DB_NAME=mydatabase

COPY . .

CMD python app.py