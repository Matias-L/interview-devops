FROM python:3.7-slim-buster
ENV PYTHONUNBUFFERED=1
WORKDIR /backend
RUN apt-get update && apt-get install -y build-essential libpq-dev libgraphviz-dev
COPY requirements.txt /backend/ 
RUN pip install -r requirements.txt
COPY . /backend/