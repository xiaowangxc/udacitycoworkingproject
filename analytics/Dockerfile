FROM python:3.8-slim-buster

WORKDIR /src

COPY ./requirements.txt requirements.txt

RUN 
# Update the local package index with the latest packages from the repositories
apt update -y && \

# Install a couple of packages to successfully install postgresql server locally
apt install build-essential libpq-dev -y && \

# Update python modules to successfully build the required modules
pip install --upgrade pip setuptools wheel -y && \
pip install -r requirements.txt && \
kubectl port-forward service/postgresql-service 5433:5432 & && \
export DB_USERNAME=myuser && \
export DB_PASSWORD=mypassword && \
export DB_HOST=127.0.0.1 && \
export DB_PORT=5433 && \
export DB_NAME=mydatabase && \

COPY . .

CMD python app.py